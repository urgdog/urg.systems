---
title: Google Docs Why
date: 2025-06-01
layout: default
---

# Google Docs Re-Oriented for People Who Care (too much?)

## Problem: 
"Why the is there random whitespace after I hit enter sometimes? Especially lists?"

## Answer:
You're falling into 'normal text' styles (little dropdown, left of 
the font). Docs seems to presume that you're writing your next big breakout novella
and wants gigantic paragraph spacing by default. Why? idk. Let's fix it 
so the enter key behaves normally.

## Solution: 
1. Open a fresh doc. Paste this in:
```Title
Subtitle
Heading 1
Heading 2
Heading 3
Heading 4
Heading 5
Heading 6
```

2. Click each line, then apply the matching style from the style dropdown (e.g., 
"Title" for the title line).

3. Select everything `(CTRL+A)` then go to  `Format > Line & Paragraph Spacing >
Custom Spacing`.

4.  Set the **Before** and **After** boxes to **0**. Leave **Line Spacing** at 
**1.15** unless you want tighter line spacing.

5. Hit **Apply**.

## Make It Stick:
- Open the style dropdown, scroll to the bottom.
- Click `Options > Save as my default styles`.

This now applies to all _your_ new docs.

## Caveats: 
- This won't affect shared docs you didn't create (prolly obvious but just sayin'.)
- Pasting in styled text from someone else's Docs dumpster fire may "pollute"
your now superior, clean, and controllable styles.
- Use `CTRL+SHIFT+V` to paste as plain text to keep your stuff clean to avoid that.

If a doc gets janked up, just redo the fix above - it will bend back to your will.

