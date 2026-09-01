---
date: 2026-09-01
title: Save a round trip
tags: [tech, quic, firefox, networking, http3, dns]
---

Most sites that serve HTTP/3 do not use it on the first connection: the browser has to discover it, wasting a round trip. One DNS record fixes that.

I built a small tool to check any domain: [savearoundtrip.com](https://savearoundtrip.com).
