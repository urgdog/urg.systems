---
title: Downtime / Quad Size Ratio
date: 2025-05-11
layout: default
---

# DQR Theorem:

In any sufficiently large network environment, the physical effort expended
per unit of downtime is inversely proportional to the intelligence of the
maintenance plan.

This is the "Downtime to Quadriceps Ratio", or DQR.

Formally:

> D = Q * SR

Where:

```
D = Total downtime (seconds)
Q = Average quadriceps size of engineers on-site (cm)
SR = Squat ratio- the percentage of devices in the lower third of racks within the 
maintenance scope.
```

Therefore, as Q increases (beefy field engineers from repeated squats) and SR remains
high (lots of low gear) you can predict your downtime to also be high, unless
mitigated by strategy.

---
Origin Story of the DQR:

Most 'planned' maintenance I've encountered seems to be created by people that
never held a pair of cutters, and probably weren't allowed 300 feet
within a data center anyway.

Or, more charitably: people who never dealt with the other end.

SOP would sequence upgrades by port, numerically. 
Going by port on the gear means you're doing 300 squats a night.

So, why not go by rack? Turns out nobody had bothered to put where the stuff
was located. Why? I don't know. If it existed, it wasn't available.
Unfortunately there is a LOT of random weird gear in these
places, so it's kind of hard to systemize it, but it's also not THAT bad to
do it in "reverse" (ie, just use your eyeballs and a spreadsheet)

So before each maintenance, I'd walk through and map gear to a
spreadsheet. Sort that sheet by rack and print.

Then I'd hand em out to the techs:

> "These are your racks tonight. Stay in them. Everything you need is here. Follow the sheet."

Ofc the aged veterans looked suspiciously at my dark art- "what if it didn't work?
what if we miss one?"

> "If sorting a spreadsheet randomly deleted information, we should prepare
for the collapse of global finance. Because banks run on excel, which is 
stupid and horrifying, but a topic for another day. Just trust me on this."

A few skeptical grumbles aside, one night, we ran a maintenance so cleanly
it didn't even show up on the outage report. It was assumed we had canceled it,
which was neat.

This isn't genius work- in fact I'd fully expect you to say "obviously".

That's kind of the point - it's super obvious, it had never been done because
it had just never been done before and nobody bothered to check.

<div class="field-box" style="white-space:pre-line">
Don't ignore the simple stuff.  
Sometimes there's reasons to do it "the long way", and that's ok.  
But you should know *why* before repeating it.  
Some reasons are good. Some are just old and not worth doing anymore.  
Figure it out and get lazy.  
Not beefy calves.  
</div>
