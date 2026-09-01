---
date: 2026-03-18
title: Talk "Happy Eyeballs v3 in Firefox" @IETF 125
tags: [tech, talk, firefox, networking, happy-eyeballs]
ShowToc: true
TocOpen: false
---

I presented Firefox's Happy Eyeballs v3 implementation in the [HAPPY working group](https://datatracker.ietf.org/wg/happy/about/) at IETF 125 in Shenzhen.

At that point the implementation had landed in Firefox Nightly, still off by default and reachable by flipping `network.http.happy_eyeballs_enabled` in `about:config`. It followed [the draft](https://datatracker.ietf.org/doc/draft-ietf-happy-happyeyeballs-v3/) with no major deviation.

I introduced [mozilla/happy-eyeballs](https://github.com/mozilla/happy-eyeballs), the Rust library behind it: deterministic, free of side effects, abstract over I/O and time, and with no dependency on Firefox. Each scenario is a plain unit test, which makes the algorithm easy to formalize. I offered those tests to the working group as a way to pin the algorithm down.

I showed the first public telemetry on DNS lookups and connection establishment latency, where the tail is long: a median of 73 ms, but 537 ms at the 95th percentile and 1.7 s at the 99th. Those numbers are what we planned to tune the resolution and connection attempt delays against.

I closed on the plan: enable Happy Eyeballs v3 in Nightly within weeks, ship it to release within months, and bring more telemetry back to IETF 126.

[Slides](https://datatracker.ietf.org/meeting/125/materials/slides-125-happy-hev3-in-firefox-00) and [recording](https://www.youtube.com/watch?v=l9eId_Yjoew&t=4730s)
