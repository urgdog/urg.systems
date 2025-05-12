---
title: Homelabs, aka Battle Testing Reality (and Yourself)
date: 2025-05-11
layout: default
---

# Homelabs, aka reasons to make yourself feel bad

Breaking things is a great way to learn.

Scratch that. Actually, fixing them is the part where you learn. Breaking them is easy.
Just maintain the rate of fix to be higher than rate of break. That's the ideal state.

I have a little homelab that I use with real constraints that mirrors how systems fail
and survive in the real world. I use it to test automation workflows, monitoring logic,
and "Can this device can run at 80 VAC?" (Yes! For almost a minute!)

"Prod" setup, roughly:

- WireGuard site-to-site tunnels across multiple physical locations
- Dyn DNS, LTE backup links.
- UDM Pro for segmenting "prod" from chaos. If you have a WFH partner, you've got real prod. Careful.
- ~80+ Cat 6e pathed through the house. Why not?

The lab side:

- Dell/Supermicro hosts for virtualization, VMware/Proxmox
- Intel NUCs for... actually I don't remember what that one's doing.
- a few Mikrotiks (They can do everything! Why not set up BGP on a pocket calculator?)
- Digital Loggers (IP Power controlers), some UPSs, and lots of velcro. So much velcro.

It's good to dive in just to stay sharp.

If you haven't experienced the full ride of: 
> "I am the smartest person alive!"

> "I am dumber than pond scum."

> "Yes! I am a genius!"

You should probably build a lab. It will humble and enlighten. It doesn't need to be expensive.
You don't even need to know anything yet. That's the point. You just have to want to.

Next up: Maybe a weather station, or some time lapse photography. I'm sure I'll break something doing it.
[greg@urg.systems](mailto:greg@urg.systems)

