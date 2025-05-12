---
title: Building Zero-Touch Provisioning for Hardware That Didn't Want It
date: 2025-05-11
layout: default
---

# Building Zero-Touch Provisioning for Hardware That Didn't Want It

Infrastructure automation only succeeds when it accounts for the reality of field conditions,
not idealized workflows. This post explains how I build a scalable Zero-Touch Provisioning (ZTP)
platform for hostile, inconsistent hardware across dozens of vendors- and why the solution 
had more to do with aligning the tech with business than any sort of specific tooling.

---

Zero-Touch Provisioning is great- you spin up a DHCP server, some TFTP, make your golden configs.
In theory, this lets you plumb together all your business systems and it'll all just work.

Except not all gear supports this type of integration.

I've had to scale hardware that actively resists this automation- no DHCP on boot,
unpredictable reset buttons, vendor responses that border on comedy gold.

These deployments don't scale when your techs are sitting on a bucket in a basement 
asking for help via a cell-powered teamviewer connection. In all honesty, that's how it started.

So, we built a system that controlled for this 'hostile gear'- watching MAC tables, ARP spoofs,
config injection reboot and pray (why did that one take 3 minutes and not 1?) Some of it was fragile,
some of it turned out way more robust than I could have expected. Integrating the business into a
ZTP platform with this equipment, where the state could be unknown was a wild ride.

At the end of this, we got a tremendous amount of optimization done using the custom ZTP bootstrapping
and processes we built.

It worked because we designed it around **how the field actually works**, not how a vendor thinks it should work.
Automation paved over hardware oddities, and we had a very solid environment that people relied on to 'just work'.

The hardware would never cooperate- that's a given.

But we have Turing-complete programming languages.

Checkmate.

---

Want to talk some gritty details about how to get a serial number on a sticker in a basement associated
with software on that box without going there and looking at the sticker? Oh, btw the serial number
is not loaded anywhere in the software. Intrigued? [greg@urg.systems](mailto:greg@urg.systems)

