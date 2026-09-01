---
date: 2026-07-20
title: Talk "A Report on Firefox's HEv3 Implementation" @IETF 126
tags: [tech, talk, firefox, networking, happy-eyeballs]
ShowToc: true
TocOpen: false
---

I reported on Firefox's Happy Eyeballs v3 implementation in the [HAPPY working group](https://datatracker.ietf.org/wg/happy/about/) at IETF 126 in Vienna.

Happy Eyeballs v3 races connection attempts across address families and protocols and keeps the first one that connects. Since IETF 125 it is enabled by default in Firefox Nightly, reaching roughly 15k users.

The implementation is a library of its own, [mozilla/happy-eyeballs](https://github.com/mozilla/happy-eyeballs): a deterministic, sans-I/O state machine in Rust with no network and no clock. The caller drives the I/O and passes time in. It does not depend on Firefox, it embeds in Necko's C++ event loop, and every scenario is a plain unit test.

I walked through the ten public [Glean](https://glam.telemetry.mozilla.org/fog/probe/netwerk_happy_eyeballs_end_to_end_time_succeeded/explore) metrics we now collect in Nightly. From the first DNS query to a connected socket the median is 74 ms and the 95th percentile 603 ms. 84% of connections are won by the first attempt. Failures either fail fast or grind to the 10 s cap, with little in between.

Firefox tracks [the draft](https://datatracker.ietf.org/doc/draft-ietf-happy-happyeyeballs-v3/) closely, with two delays tuned from that telemetry: a 25 ms resolution delay rather than the draft's 50 ms, and a 50 ms connection attempt delay that doubles on each step (50, 150, 350, 750 ms) rather than a flat 250 ms.

I closed on [savearoundtrip.com](https://savearoundtrip.com), which checks whether a domain publishes an HTTPS record. Many sites advertise HTTP/3 through Alt-Svc alone, so every first visit pays a wasted round trip: connect over HTTP/2, read the header, and reach HTTP/3 only on the next connection. An HTTPS record with `alpn="h3"` goes straight to QUIC, and it is the only way to deliver ECH.

[Slides](https://datatracker.ietf.org/meeting/126/materials/slides-126-happy-update-on-firefox-implementation-00) and [recording](https://www.youtube.com/watch?v=5GaOjpjgCt8&t=2805s)
