---
title: what is iptables anyway
date: 2025-07-11
layout: default
---
# iptables, how does it really tho
Most people think they understand iptables. They don’t. Including me,
until I traced a packet through every single chain like a lunatic with
too much time and a burning desire to stop being lied to by man pages.

This is also mostly notes for myself so I can forget these details.

We start from inside a Docker container on a host, and then ping out,
and see the return packet logic.

We're going to go through a VERY simple setup, which will get you to 90%
of use cases, but should pique some interest if you want to get weirder with it.

Summary of the whole thing:

For an inbound packet:
```
NIC recv
 ↓
PREROUTING (raw, mangle, nat)
 ↓
Routing Decision:
 ├── Destination = local? → INPUT (Host firewall)
 └── Destination = elsewhere? → FORWARD (Routing THRU host, not TO it)
 ↓
POSTROUTING
 ↓
NIC send
```


<br>
And for host-origin traffic:
```
Local process
 ↓
OUTPUT (raw, mangle, nat, filter)
 ↓
POSTROUTING
 ↓
NIC send
```

| Table  | Used for                        |
| filter | Basic allow/deny firewall rules |
| nat    | Address translation (SNAT/DNAT) |
| mangle | Packet alteration (ToS, marks)  |
| raw    | Bypass connection tracking      |


Each table has chains (which are like hooks in the packet lifecycle):

| Table   | Chains                          | Purpose Example   |
| filter  |  INPUT, FORWARD, OUTPUT         | Accept/Drop       |
|  nat    | PREROUTING, POSTROUTING, OUTPUT | SNAT/DNAT         |
| mangle  |  All 5 + INPUT, OUTPUT          | Marking, QoS      |
| raw     | PREROUTING, OUTPUT              | Disable conntrack |



OUTPUT: src is from host
INPUT: dst is the host
FORWARD: Neither dst nor source on host (ie, forwarding thru)

---

## now, the walkthru
use a docker container on a host:

`docker run -it --rm --cap-add=NET_ADMIN --cap-add=NET_RAW --name urgtables ubuntu bash`

Install iptables tools in the container:  
`apt update && apt install -y iproute2 iputils-ping curl iptables`

You can put icmp into "INPUT", so you can see if you're even getting there-
you don't need this for anything to work, but it lets you see counters go up,
which can be handy just to prove to yourself what's going on:

`sudo iptables -I INPUT 1 -p icmp`

then watch input iptables:  
`iptables -L INPUT -v -n --line-numbers`


If you need to clear counters:  
`iptables -L -Z -v`

Somewhat repeating above, but these are the tables a non-routed packet takes.
Don't worry if you run these and you don't get it yet, just showing a 
general idea:

You generally wont have things in `mangle` or `raw`. But you will have something in `nat`.

- `iptables -L PREROUTING -t mangle -n -v --line-numbers` 
- `iptables -L PREROUTING -t raw -n -v --line-numbers`
- `iptables -L PREROUTING -t nat -n -v --line-numbers`

You'll probably just see a couple rules here, like a DOCKER chain and maybe nothing
matching your traffic yet. That's fine. This chain only catches traffic that
needs NAT handling at this point (e.g. published ports or DNAT).
Most flows won’t match here unless you’ve exposed something.


If Docker’s in play, you’ll see a `DOCKER` chain in nat - it handles published ports.
- `iptables -t nat -L DOCKER -n -v --line-numbers`

and then `INPUT` if you're local (ie, not needing to route):
- `iptables -L INPUT -v -n --line-numbers`

You’ll see the packet counters tick up here if your host is the final destination.
But if you're routing (e.g. from container ➝ internet), this chain won’t get hit.
Handy way to prove "am I being addressed directly?"


Then `POSTROUTING`:
- `iptables -t nat -L POSTROUTING -v -n --line-numbers`

Remember, INPUT is from things outside the host, which would apply for a docker
container.

---

### For a routed packet:
Starting at the same thing, prerouting, then probably DOCKER:

- `iptables -L PREROUTING -t mangle -n -v --line-numbers`
- `iptables -L PREROUTING -t raw -n -v --line-numbers`
- `iptables -L PREROUTING -t nat -n -v --line-numbers`

- `iptables -t nat -L DOCKER -n -v --line-numbers`

There generally isn't MUCH in the `DOCKER` chain, but for completeness let's dig in there
and make sure the rules aren't borked.

Look at the actual routing table on the host:  
`ip route get 1.1.1.1` (or whatever IP you're tracing)

Then we will likely wind up in FORWARD:  
`iptables -L FORWARD -n -v --line-numbers`

This is where docker puts a lot of its rules, so you'll likely see `DOCKER-USER` and `DOCKER-ISOLATION-STAGE-1`, which we can then inspect those rules:

`iptables -S DOCKER-USER`  
`iptables -S DOCKER-ISOLATION-STAGE-1 `

These rules say, roughly: if traffic enters from a Docker bridge and is headed somewhere else, it gets flagged for stage 2 isolation.
e.g.,
<pre>
-A DOCKER-ISOLATION-STAGE-1 -i docker0 ! -o docker0 -j DOCKER-ISOLATION-STAGE-2  
-A DOCKER-ISOLATION-STAGE-1 -i br-1cbda01ee2d7 ! -o br-1cbda01ee2d7 -j DOCKER-ISOLATION-STAGE-2  
</pre>

I'll show you stage 2 in a sec, but functionally this whole chain sums up as
"are you coming from a docker bridge, going anywhere else? and if you are 
going anywhere else, are you going to ANOTHER docker bridge?"
That's not allowed by default.

I'll mention this a few times, because this looks like a lot of rules to do something
that is objectively pretty simple isolation, but understanding it can potentially
unlock some neat concepts.

--- 

So! What's stage 2 doing? Let's look:  
`iptables -S DOCKER-ISOLATION-STAGE-2`

You'll see something like this:
<pre>
-A DOCKER-ISOLATION-STAGE-2 -o docker0 -j DROP
-A DOCKER-ISOLATION-STAGE-2 -o br-1cbda01ee2d7 -j DROP
</pre>

Stage 2 is where Docker actually slams the door - traffic targeting other bridges gets dropped here. Docker doesn't want you to cross Docker
networks (by default). So thus far, you're saying "I'm coming from inside my
container, to ens160 (a physical nic, the path out dictated by the routing table)"
and we're here asking "is ens160 = any of these interfaces?"  

Nope. If our destination was another docker network bridge, that would mean
we're trying to go cross-docker network and will be `DROP`ped.

> as an aside: you can still reach the GATEWAY of other docker
network from inside a container. This is notable because you can know about
the existence of other networks from inside a container. This CAN be bad news.
90% of the time, it's not a big deal though- but good to be aware of if it's
part of a security gap you want to fill.

---

So, based on our routing table, `ip route get 1.1.1.1` and got ens160 as our dest iface,
we'd say- I'm free, I didn't match the docker gauntlet.  
Let us proceed  the `FORWARD` chain:

Remember our input iface:  
`br-1cbda01ee2d7`

If we look back at our `FORWARD`, you'll see input and output ifaces that match:

<pre>
-A FORWARD -i br-1cbda01ee2d7 ! -o br-1cbda01ee2d7 -j ACCEPT
</pre>

Meaning, traffic coming from the bridge, going anywhere other than the same bridge -> ACCEPT.

This is what lets containers talk outward.

---

Now, we look at postrouting:  

`iptables -t nat -L POSTROUTING -v -n --line-numbers`

You'll see something like this:
<pre>
MASQUERADE  all  --  *      !br-1cbda01ee2d7  172.20.0.0/16        0.0.0.0/
</pre>

You can test this rule firing by running repeated pings from the container
`ping 1.1.1.1` and watching the packet count here go up. That means this rule
is rewriting the src IP on egress.


Now you've probably got a specific src-dest! This is what actually re-writes the
source to be the host's source, so we can get it back (SNAT). It re-writes the source IP,
so return traffic from the public internet will be sent back to the host, not the
container. `Conntrack` (we'll get to this in a sec) + DNAT handles return path to container.

Meaning, "The packet is not going to the bridge it just came from, and it matches this subnet (172.20.0.0/16)".

`MASQUERADE` then means: "okay, re-write this source addr to the ip of the iface the routing table told us about earlier, and send it"

And that's how iptables sends a routed packet.

---

## return path
If you've established a connection from a container, out thru the internet, it
will be in conntrack:

`conntrack -L`

Try pinging from the container to 1.1.1.1 and immediately run conntrack -L.
You'll see a line with protocol icmp, and it’ll list a src, dst, and id= field.
(ID is how it tracks ping sessions, since there are no ports in ICMP).

now when a return packet comes back, it looks at conntrack and says "ah, I have rx'd a
thing matching what I previously sent out using src/dest ip, src/dest port
and protocol".

NOTE! You won’t see a MASQUERADE rule hit here on return, because it already matched and 
got recorded in conntrack (when we were going out). This is why return packets
don’t need to "undo" MASQUERADE manually.

Anyway, we send this back into iptables-

PREROUTING first!  
`sudo iptables -S PREROUTING -t nat`

We see:
<pre>
-P PREROUTING ACCEPT
-A PREROUTING -m addrtype --dst-type LOCAL -j DOCKER
</pre>

And we can interpret "yup, the destination is local, from the internet, because the target is the host itself!"

---

So we look at the DOCKER chain:  
` iptables -t nat -S DOCKER`

You'll see something like this:
<pre>
-N DOCKER
-A DOCKER -i docker0 -j RETURN
-A DOCKER -i br-1cbda01ee2d7 -j RETURN
</pre>

If you're publishing ports, these will be different. Without that, we're just saying
"is my "-i"nput interface any of these? (ens160)" Nope.

Also to note, `-N DOCKER` is really just a command saying "make a new chain called
`DOCKER`" - the very thing you're looking at.

---

We look at FORWARD now:  
`iptables -S FORWARD -v`

Note this chunk again:
<pre>
-A FORWARD -o br-1cbda01ee2d7 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -o br-1cbda01ee2d7 -j DOCKER
-A FORWARD -i br-1cbda01ee2d7 ! -o br-1cbda01ee2d7 -j ACCEPT
-A FORWARD -i br-1cbda01ee2d7 -o br-1cbda01ee2d7 -j ACCEPT
</pre>

Specifically the first one which means:

hey `conntrack`, if you've got any established connections, accept it.

But wait, you'll say- the packet's destination is still "the host", not the container.
How do we know where it's going?

That is what `conntrack` just did by hitting that `FORWARD` rule successfully.
This is where the magic happens I mentioned earlier. `conntrack` remembers what
outbound connections you made, so the return packets know how to get back.

return path = no more MASQUERADE, just a conntrack-validated return trip
through FORWARD + POSTROUTING.

It will then proceed into `POSTROUTING`- where again, nothing will match,
so it will pass thru without incident.

Once you're past `POSTROUTING`, now you're back to the interface, and off to the container!

And that's how packets get out of a conatiner, and back into a container.

So: if you're looking to use Docker without punching holes through your host, understanding
these chains lets you do that without hoping Docker’s abstraction does the right thing.
