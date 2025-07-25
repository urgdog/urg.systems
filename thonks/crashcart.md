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
    When that link dies, search: `"USB 3.0 Video Capture Card 1080P HDMI UVC"`  
  - **Rii Mini Keyboard** 
    - [Link](https://a.co/d/brLzEnv) - Rechargeable, works with everything. Or use any USB keyboard/mouse if you hate fun.
  - **HDMI cable** 
    - Just enough to get to your laptop from a top-of-rack server. A few meters.

  - **Optional:** [VGA to HDMI adapter](https://a.co/d/7Ac4gSm)  
    - For VGA equipment. Pick one with USB power. That means it's active, which you need. Direction matters. Passive adapters won't work.

  - **Mandatory:** Velcro straps
    - If you don’t own these already, I don’t know what to tell you. Actually, I do.

## 3. How It Works

1. Plug server HDMI -> USB capture card  
   (Use VGA adapter if applicable)

2. Plug capture card -> laptop (USB-A or USB-C)

3. OBS or any webcam viewer picks it up instantly  
   OBS, VLC, ffplay - whatever. Shows up like a webcam, which means you could 
   even share it over Zoom... for some reason.

4. Plug in your keyboard -> you're in.
   Watch your server boot, panic loop, or whatever.

Around $60. No more begging for a crash cart.
No more VGA monitor in your closet.
You are the crash cart now.
