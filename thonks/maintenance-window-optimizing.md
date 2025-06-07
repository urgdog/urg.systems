---
title: Downtime / Quad Size Ratio
date: 2025-05-11
layout: default
---

# Downtime / Quad Size Ratio Theorem:

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

Therefore, as Q increases (beefy engineers from repeated squats) and SR remains
high (lots of low gear) you can predict your downtime to also be high, unless
mitigated by strategy.

---
Origin Story of the DQR:

Most planned maintenance I encountered early in my career was... polite. Engineers would
sequence upgrades by port, numerically and hope that we could get it done before the window
closed. It was clean and easy from the engineer's perspective.

But it also meant I was doing 300 squats a night.

But I don't need legs the size of tree trunks to work in a data center. That
probably becomes a liability at a certain point.

So, why not go by rack? Turns out nobody had bothered to put where the stuff
was located in the headends. Why? I don't know. If it existed, it wasn't 
readily available. Unfortunately there is a LOT of random weird gear in these
places, so it's kind of hard to systemize it, but it's also not THAT bad to
do it in "reverse" (ie, just use your eyeballs and a spreadsheet)

Before each maintenance, I'd walk through and map the  involved gear to a
spreadsheet. Sort that sheet by rack and print out the sheet. (I carried a printer
in my truck exclusively for this purpose)

Then I'd hand out the sheets to techs: 

> "These are your three racks tonight. Stay in them. Everything you need is here. Follow the sheet."

Ofc the aged veterans looked suspiciously at my dark art- "what if it didn't work?
what if we miss one?"

> "If sorting a spreadsheet randomly deleted information, we should prepare
for the collapse of global finance. Or, I screwed up and we'll find it about 4
hours faster anyway."

A few skeptical grumbles aside, doing this sliced our downtime viciously.

One night, we ran a maintenance so cleanly it didn't even show up
on the outage report. My boss assumed we had canceled it. Nice.

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
