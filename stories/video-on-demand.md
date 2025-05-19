---
title: Troubleshooting Video On-Demand
date: 2025-05-10
layout: default
---

This is a story about troubleshooting video on-demand, in the olden days.


### Technical Junk, not 100% needed but explains some fun trivia:

---

First, some backstory on a little bit of the technical components of how
video on-demand USED to work in a cable environment, before the days of IP-based
video, and when every TV had a "set top box" of some kind. The purpose of this 
box was to translate the digital cable signal into something the TV itself
could understand.

So, some of you ancient-timers may say "that's not that old, back in my day
you could plug a piece of coax directly into the tuner of the TV!"

Yes, I know, I remember, I worked then too. That was before VOD.

Anyway, these set-top boxes had rudimentary communication channels- remember,
the entire architecture was BASED around broadcast (thematically, not in the IP sense)
so there was a lot of "plug it in and wait for the data to be broadcast again"
and "wait 10 minutes for the thing to load" because EVERYONE was receiving the same
control/interface data, all the time, forever, on loop. This particularly
applies to things like the On-Screen TV Guide, which would take a while to load.

Same thing would apply for the VOD interface.

When the set top box would request a VOD, the request send a signal through the
authorization system, and then, if authorized, there's a special box that
specifically modulates video onto a carrier in the headend- just like any other
typical broadcast channel, but these frequencies are designated for VOD.

Technically speaking, the "VOD" is also broadcast to everyone on the wire, but only the set-top box that requested it can access it through a cryptographic forward-only system. Don't quote me on the details there, it's been a while.

This makes it (in theory, I think) impossible for any random set top box to tune
to VOD streams in progress in their area.

All of this is to say, the set top box is really just saying "I wanna watch a thing,
and I'm going to look at a frequency to do it" and the backend system is saying 
"someone in that area wants to watch a thing, we will broadcast it on a specific
frequency."

Now, you might think this broadcast thing is what this story is about- it's not.

It's really about the authentication method- it was very janky, there was a lot
of local controls to prevent abuse stacked on top of remote controls. In essence,
this all means "on demand can act weird based on the model/firmware of set top box
and only Lord Motorola himself can tell you what's going on".

Ok, that's enough tech gunk. Onto the story.

---

## The story, for real this time

I worked nights with another tech in the area I supported- just the two of us
most nights. (Nights as in, our shift ended at 19:00, not true overnights).
As is tradition for any individual field work, if you finish up
early, you call the other guy to see if they need a hand, and vice versa.

I don't know if that's how it works these days, but I hope it still does.

I had finished my job up early, and I called my buddy- he had one more,
on my way home. We didn't get a ton of details on the issue, mostly a category
of some type. This one said "VOD" (Video On-Demand). Ugh. Those could be annoying,
for tons of various reasons (or they could be super easy). Worth rolling to.

We both arrived at around the same time, it was getting dark outside. We knocked
on the door, and a young guy answered the door. We introduced ourselves,
confirmed that we're at the right place, and he invited us in.

He had the typical setup you'd expect from a mid-late twenties guy. Not super
clean, not a disaster. No red flags for sure.

For the conversation, we'll call the subscriber Jake and my co-worker we'll call
Bob.

> Me: "So, you're having on-demand issues?"  
> Jake: "Yeah, so... it's kind of weird, sometimes it works just fine..."  
> Me: "Oh, that's annoying- ok, well let's see if we can get it to happen now"  

Bob was already on it, clicking through the menus loading up a free On-Demand movie.
Loaded up just fine, movie starts playing. Ugh. Intermittent problems are the worst.

Jake piped up- "well, it only really seems to cause a problem with the ones 
you pay for."

"Interesting." maybe a hold on the account? Sometimes that happens if there's a
TON of videos ordered, they'll just block the box.

Bob clicked through the interface, looking for a premium VOD (like a recently released movie).
We'd credit the account, so no biggie there. Loaded up just fine, started playing.

From the couch, Jake said, "Well, not those... We tried this on the phone,
those always work."

I raised an eyebrow. "So premium VODs always work? And free VODs always work?
Wait a sec, when doesn't VOD work?"

"Oh, well, you know, like... the... I mean, I can show you."

Jake took the remote, and navigated the VOD menu to the Adult section.

My first reaction was technical incredulity- why would the back end system
care? We just ordered a movie you have to pay for, what's the difference with
adult VOD? Technically nothing, as far as I know...

Jake selected a feature I don't remember the name of, and I will spare you.

Sure enough, an error popped up on the screen, but it looked like a technical
error. Granted, there were hundreds of VOD errors, so who knows what the actual
error related to- it definitely just didn't work.

Jake did a few more- none worked- same error.

We tried another "regular" premium VOD- worked just fine.

I said, "Ok, so this feels like an account-level block or something. Let me
call dispatch and they can dig a little further in here."

I called dispatch and got Erin. I was thrilled, she really knew her shit-
which was absolutely necessary to navigate whatever odd pile of nonsense we
were looking at. I described the problem to her, and she said "Yeah, I see
a LOT of orders recently."

"Yeah, that's probably us testing- gonna need to credit those.. but none of those
actually came up as viewable. Is there anything blocking the account from adult
VOD?"

"I don't see anything," Erin replied, "but give me a few, these can be weird."

Awesome. Few minutes go by, she comes back.

"Everything looks fine... I did clear out those purchases, so he won't get
charged for... yeah that was a lot of purchase attempts."

Well, ok- this has to be a device specific hardware issue now- Bob was already
a step ahead of me, he was getting a new set top box from his truck.

He swapped the box out, and I stayed on the phone with Erin, as we were the only
ones in the field still, and we'd need to credit any further testing we did, and
I didn't want to call back and get someone else without context of this thing.

We waited about 5 minutes for the box to load up the VOD menus.

Bob went to the Adult VOD menu, and randomly selected a feature which, 
if I remember correctly, was something along the lines of "Fun at the Beach".

What I do remember, was this feature did not waste time at all on exposition.
Straight to action- very efficient. Also, it was a gay feature. Not that there's
anything wrong with that, of course. Just not the kind of data payload you're
expecting to be verifying.

Erin remarked from our audibly shocked reactions, "Sounds like it's working?"

> Me: "Yes. Yes it is. Can you credit that? The customer does not want to watch it."  
> Erin: "Yup, all set. Anything else you need help with?"  
> Me: "Nope."  

So we packed up our gear and went on our way, another problem solved, one more
awkward situation under the belt.

<div class="field-box">
And that's how I got paid for going to a stranger's house with a co-worker,
calling a woman, and watching gay porn.
</div>
