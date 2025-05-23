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

But as a co-worker said: "There's no please or thank you in the maintenance window."

He was right- these port-by-port methods were just too polite. It also meant I was doing
300 squats a night at least. 

But I don't need legs the size of tree trunks to work in a data center.
In fact that probably becomes a liability at a certain point.

The problem wasn't complex- **the interface has nothing to do with the rack location**. 
The source port might be 1/0/5, but that doesn't tell you where the cable work is.
So the ‘logical’ order translated to a lot of walking, squatting, and wasted time.

As we already know, this causes massive gains in quads, and consequentially, downtime.

I suggested going by rack- the response was 

> "We can't, we don't know where everything is. It'd take too long." 

I said, "I've got a spreadsheet, a wireless keypad, and eyeballs. Give me an hour."

Before each maintenance, I'd walk through and map the gear to the spreadsheet.
Sort that sheet by rack and hand out the new, physical-first migration plan.

> "These are your three racks tonight. Stay in them. Everything you need is here. Follow the sheet."

This sliced our downtime viciously. One night, we ran a maintenance so cleanly it didn't even show up
on the outage report. My boss assumed we had canceled it.

We performed so well that impact wasn't even known.

This isn't genius work at all, I'm not expecting any accolades- in fact I'd fully
expect you to say "obviously".

That's kind of the point - it's super obvious, it had never been done because
it had just never been done before. Something as simple as using a spreadsheet
to sort some data fundamentally changed what was just SOP for years.

<div class="field-box" style="white-space:pre-line">
Don't ignore the simple stuff. Sometimes there's reasons to do it "the long way", and that's ok- but you have to understand why they're done a certain way before you can optimize.

The reasons could also simply be lousy- steeped in ancient tradition that is no longer relevant.  

That's what gets you that next step of insight.  
</div>
There are better ways to get tree-trunk calves than squats in a poorly mapped DC.  