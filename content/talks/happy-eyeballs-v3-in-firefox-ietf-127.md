---
date: 2026-11-16
title: Talk "Happy Eyeballs v3 in Firefox" @IETF-127
tags: [tech, talk, firefox, networking, happy-eyeballs, http3]
---

I gave an update on Happy Eyeballs v3 in Firefox at the HAPPY working group session at IETF 127.

Since IETF 126, Happy Eyeballs v3 is on by default in Nightly and rolled out to 50% of Release. A Release experiment on Firefox 160 compared it to a control group. Page loads on a new connection used HTTP/3 more often, 24.6% instead of 19.6%, and first contentful paint was faster at every percentile. I also covered the two delays the draft adopted from Firefox: a 25 ms Resolution Delay and a 50 ms Connection Attempt Delay that doubles with each attempt. Then the recent changes: Optimistic DNS, and HTTPS records with IP hints. I closed with what Happy Eyeballs enables next: a persistent DNS cache, optimistic Alt-Svc, and racing HTTP/3 without any prior signal.

- **Slides: [mxinden-bot.github.io/slides/14-hev3-ietf127](https://mxinden-bot.github.io/slides/14-hev3-ietf127/)**
- **Recording: [youtu.be/z7cGDl6DjcQ?t=2501](https://youtu.be/z7cGDl6DjcQ?t=2501)**

Feedback welcome, either on [mozilla/happy-eyeballs](https://github.com/mozilla/happy-eyeballs/issues) or via mail.
