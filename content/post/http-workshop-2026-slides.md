---
date: 2026-07-17
title: Slides from the HTTP Workshop 2026
tags: [tech, quic, http3, firefox, networking]
---

I gave three short talks at this year's [HTTP Workshop](https://github.com/HTTPWorkshop/workshop2026).

## Increase and evolve HTTP/3 & QUIC

**Slides: [mxinden-bot.github.io/slides/04-quic-discussion](https://mxinden-bot.github.io/slides/04-quic-discussion/)**

A discussion deck. HTTP/3 sits around 30% and has plateaued. I cover the ways to measure that share. Then what holds adoption back: server and framework support; "security" software and enterprise middleboxes that break QUIC; and the server-side performance gap to TCP. I raise QUIC v2 as an anti-ossification concern, barely deployed. I close on the HTTP/3-native use cases (WebTransport, Media over QUIC, MASQUE) and the two ways to reach HTTP/3, Alt-Svc and HTTPS records, with the latter preferred.

## Rollout of Happy Eyeballs v3 in Firefox

**Slides: [mxinden-bot.github.io/slides/03-hev3-workshop](https://mxinden-bot.github.io/slides/03-hev3-workshop/)**

Happy Eyeballs v3 races connection attempts across address families and protocols. It keeps the first one that connects. This talk covers enabling it by default in Nightly. It walks through various relevant public Glean metrics: end-to-end time, winning attempt index, HTTP/3 discovery, and what HTTPS records carry. It presents the reusable, sans-I/O [mozilla/happy-eyeballs](https://github.com/mozilla/happy-eyeballs) library. And it shows where Firefox's tuned delays deviate from the draft, plus the edge cases hit along the way.

## Modern UDP I/O for Firefox in Rust

**Slides: [mxinden-bot.github.io/slides/02-udp-io](https://mxinden-bot.github.io/slides/02-udp-io/)**

Firefox's UDP I/O was built on NSPR's aging `sendto` and `recvfrom`, one datagram per system call. This talk covers replacing that stack with modern system calls. `sendmmsg` and `recvmmsg` batch datagrams. GSO and GRO offload segmentation. It builds on the [quinn-udp](https://github.com/quinn-rs/quinn/tree/main/quinn-udp) library, in Rust, for memory safety. I cover the throughput and CPU wins, and the per-OS quirks (Windows USO/URO, macOS's undocumented `sendmsg_x`, Android's `socketcall` and seccomp). ECN support came along for free. There is a longer write-up in [Fast UDP I/O for Firefox in Rust](/post/fast-udp-io-in-firefox/).

Feedback welcome.
