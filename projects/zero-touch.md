---
title: Zero-Touch Provisioning for Spiteful Vendors
date: 2025-05-11
layout: default
---

# Zero-Touch Provisioning for Spiteful Vendors

So, Zero-Touch Provisioning- wonderful idea when the vendor actually wants it.

This isn't that. This is a journey to the land of hostile hardware that would
sooner emit its secret magic smoke than ask for a DHCP lease. I won't
name names.

So, as you may know, most ZTP deployment guides are written for
someone discovering Linux for the first time.

> "My first Linux: deploy `isc-dhcpd`, a TFTP server, and
some config files and firmware files, etc."

I appreciate the guidance, but `isc-dhcpd` was EOL in 2022 and TFTP over
PTMP RF? I can DoS my own network without your help, thank you.

And those are the "good" ones. At least with that I know there's something
I can work with.

What I'm talking about are the ones that need to work at massive scale, and
have aspects of technological cryptozoology like:

> No DHCP on any interface, even after reset  
> A "factory reset" button that... just reboots.  
> Serial numbers on stickers only. Not in software.  
> and of course, no MAC address labels anywhere.  

We need this whole pile to work where remote hands MIGHT be
able to string up a teamviewer session on a cell hotspot, an hour away from 
any warehouse. At best.

So, for this particular hellscape, we dove in deep.

So we built a bootstrapping system that never presumed state.
We had to get in there SOMEHOW (via serial, old IP, whatever).
Gave it a baseline configuration, used SNMP probing/MAC tables
to figure out what we were talking to, and pulled a lot of historical data
into something resembling a serial tracking system.

The amount of conditionals in a permanently stateful system are obnoxiously
staggering, to say the least. But, with a little bit of field wisdom, and
knowing how things actually work in the real world, and a lot of pencil and
paper diagrams (and erasers), we were able to get this thing into a state
that actually behaved like a rational piece of hardware.


<div class="field-box" style="white-space:pre-line">
If you're looking at a beast of this magnitude, and somehow you're also reading this- you've got this.  

It will be painful and someone will somehow upend piles of assumptions you made, but it can be done.
 
Iterate and stay close to the output.
</div>

We even hacked together a ‘remote reset’ workaround just to give the illusion
of a sane provisioning cycle.

There are tons of other details I'm glossing over here- but the end result was
that this thing worked for the org. It wasn't pretty in the traditional sense.

It was godly in terms of decades of experience controlling "what if...".

Which is really what resilience looks like deep down- **weaving the chaotic fabric
of reality into something that looks like it was meant to fit the rack.**
