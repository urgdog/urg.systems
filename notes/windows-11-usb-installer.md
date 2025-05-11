---
title: Windows 11 USB Install - "Load Driver to Show Hardware"
date: 2025-05-10
layout: default
---

# Windows 11 USB Install - Install Driver to Show Hardware

BLUF: Seeing a weird "Install Driver to Show Hardware" when installing Windows 11?
Try a different USB stick - a different brand particularly.

** That is all, if you want to continue reading, do so at your own peril; no actionable
information follows. **

I had reasons to reinstall Windows 11 (24H2) on one of my machines today, which
meant looking through the bin of USB install disks and hoping there's one already
set up for Windows 11.

I initially used the "dummy windows installer" to create my USB disk, thinking that
would be the fastest way to get going. When I ran into that error, I figured
the Windows installer was trying to do something odd, as dummy installers are 
wont to do. I tried Rufus with an ISO, to no avail- same issue.

I used another USB stick- same issue. 
I used them to install Debian on the very machine I'm writing this on.
So clearly they're not totally junk.

Regardless, I was about ready to search the darker locations on the web for a 23H2 ISO,
but I decided to burn the 24H2 ISO to a different brand of USB while I carefully navigated
a series of "trust me bro it's legit here's the hash it's fine" forum posts.

I gave the install one more try, and it went through, no issues!

What is most curious to me is the fact that the Windows installer starts, but then
reports that it can't read the very USB that it used to launch the code it's using.

I regret to inform you I have no clarity on why this works — but it did.
So if you're stuck: try a different USB brand. It's dumb, but it's Windows.

-G
