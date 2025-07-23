---
title: mobile crash cart in your backpack
date: 2025-06-20
layout: default
---
# BYO crash cart

TL;DR, get a cheap streaming capture card, a tiny keyboard, HDMI cable, and OBS on your
laptop. You now have a more reliable method of consoling into servers than most colo carts.

## 1. Why This 'Guide' Exists
  - Colo or data center crash carts are unreliable/broken, or missing.
    - "Does this monitor even work or is my sever dead?"
  - You really only need HDMI in, keyboard/mouse out, and a screen you control
  - Carrying your own gear means you don't need to rely on luck to get what you need.

## 2. What You Need:
  - **USB UVC capture card** ($15-$25) 
    - Make sure it supports 1080p@30fps. I use [this one](https://a.co/d/aPj0fhj).
    When that link dies, search for: `"USB 3.0 Video Capture Card 1080P HDMI UVC"`  
  - **Rii Mini Keyboard** 
    - [Link](https://a.co/d/brLzEnv) - classic, rechargeable, decent range, works with everything. Or any keyboard/mouse. Rii's are great though.
  - **HDMI cable** 
    - Just enough to get to your laptop from a top-of-rack server. A few meters.

  - **Optional:** [VGA to HDMI adapter](https://a.co/d/7Ac4gSm)  
    - For when you're dealing with VGA equipment. When that link breaks, look for ones that include **USB power**. This usually indicates it's an **active VGA -> HDMI** converter (not HDMI -> VGA).  
    Direction matters, and passive adapters won't work for VGA-to-HDMI.

  - **Mandatory:** Velcro straps
    - You already have these. So coil this little adapter bundle up nice.

## 3. How It Works

1. Plug server HDMI -> USB capture card  
   (Use VGA adapter if applicable)

2. Plug capture card -> laptop (USB-A or USB-C)

3. OBS or any webcam viewer picks it up instantly  
   (VLC, ffplay - heck you can Zoom/Webex/Google Meet it if you want, which
   now you can even record with the meeting fuctions! slick.)

4. Plug in your keyboard -> you're in.
   Watch your server boot, panic loop, or whatever.

For around **$60**, you will never again:
- Wander a datacenter begging for a crash cart  
- Keep a dusty VGA monitor in your closet "just in case"

This is gear investment that gives you **zero-dependency console access** anywhere you go.
You are now the crash cart.
