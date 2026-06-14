---
title: Resume
author: Max Leonard Inden
---

## Experience

### Software Engineer at Mozilla

June 2024 - now

Core contributor to Firefox's QUIC / HTTP/3 networking stack: [`neqo`](https://github.com/mozilla/neqo) (the Rust QUIC implementation), its integration into Firefox, and related open-source libraries.
Across both Mozilla engagements: 378 pull requests and 500+ code reviews on `neqo`, 100+ commits to Firefox, and 17+ shepherded `neqo` releases (v0.9.0 to v0.25.0).

- **Multi-gigabit UDP IO.** [Rewrite](https://bugzilla.mozilla.org/show_bug.cgi?id=1901292) Firefox's legacy NSPR-based UDP IO path as a modern, memory-safe Rust stack on top of [`quinn-udp`](https://github.com/quinn-rs/quinn/tree/main/quinn-udp), [rolled out](https://bugzilla.mozilla.org/show_bug.cgi?id=1901295) across Linux, Windows, macOS and Android. Multi-packet IO (`recvmmsg`), Generic Segmentation/Receive Offload (GSO/GRO) and a [zero-allocation receive path](https://github.com/mozilla/neqo/pull/2184) raised CPU-bound throughput from < 1 Gbit/s to [4 Gbit/s](https://max-inden.de/post/fast-udp-io-in-firefox/), [GSO](https://github.com/mozilla/neqo/pull/2593) alone roughly 2x.
- **Explicit Congestion Notification (ECN).** Implement [end-to-end QUIC ECN](https://bugzilla.mozilla.org/show_bug.cgi?id=1902065) — marking, reading, RFC 9000 path validation and Congestion Experienced feedback to the congestion controller — resilient to middlebox interference; ~50% of Firefox Nightly QUIC connections now run on ECN-capable paths.
- **Congestion & flow control.** Switch `neqo`'s default congestion controller to Cubic, enable QUIC Path MTU Discovery, and [stabilize stream receive-window auto-tuning](https://github.com/mozilla/neqo/pull/3314) toward the bandwidth-delay product, lifting a hard 1 MB cap (~160 Mbit/s on a 50 ms link) up to 10 MB.
- **New protocols.** Implement [MASQUE connect-udp (RFC 9298)](https://github.com/mozilla/neqo/pull/2796) and classic HTTP CONNECT over HTTP/3, QUIC datagrams, and WebTransport — letting Firefox proxy both TCP and UDP over a single HTTP/3 connection.
- **Happy Eyeballs v3.** Author [`mozilla/happy-eyeballs`](https://github.com/mozilla/happy-eyeballs) from scratch: a protocol-agnostic Rust state machine for dual-stack connection racing (HTTPS/SVCB records, alt-svc, ECH retry configs per RFC 9849, configurable delays), integrated into Firefox. Contributor to the [IETF Happy Eyeballs v3 draft](https://github.com/ietf-wg-happy/draft-happy-eyeballs-v3) itself.
- **Tooling & telemetry.** Build [criterion end-to-end benchmarks](https://github.com/mozilla/neqo/pull/1758) with CI regression detection, and introduce [Glean metrics](https://bugzilla.mozilla.org/show_bug.cgi?id=1906853) and Firefox profiler markers into the HTTP3/QUIC Rust stack.
- **Open-source maintainer.** Maintainer of [`quinn-udp`](https://github.com/quinn-rs/quinn/tree/main/quinn-udp) (45 PRs), the cross-platform UDP IO crate shared by Quinn and Firefox, resolving platform issues (Windows ARM USO, Android `EINVAL`, macOS address families) that benefit the wider Rust networking ecosystem.

### External contributor to Mozilla's HTTP3/QUIC stack

December 2023 - May 2024

- 89 pull requests to [github.com/mozilla/neqo](https://github.com/mozilla/neqo).
- Refactor client and server implementation [away from `mio` to `tokio`](https://github.com/mozilla/neqo/pulls?q=is%3Apr+is%3Aclosed+author%3Amxinden+merged%3A%3C2024-06-01+bin).
- Rewrite UDP IO path, [leveraging `sendmsg`, `recvmmsg` and `GRO` via `quinn-udp`](https://github.com/mozilla/neqo/pulls?q=is%3Apr+is%3Aclosed+author%3Amxinden+merged%3A%3C2024-06-01+quinn-udp).
- Replace mozilla-central's `http3server` custom UDP IO stack, reusing new IO stack in [github.com/mozilla/neqo](https://github.com/mozilla/neqo) instead. See [bugzilla#1895319](https://bugzilla.mozilla.org/show_bug.cgi?id=1895319).
- Report and fix security vulnerability due to unbounded memory allocation based on unsanitized network input. See [bugzilla#1875701](https://bugzilla.mozilla.org/show_bug.cgi?id=1875701) and [CVE-2024-2613](https://www.mozilla.org/en-US/security/advisories/mfsa2024-12/#CVE-2024-2613).
- Fix cross-layer race conditions, see e.g. [github.com/mozilla/neqo#1819](https://github.com/mozilla/neqo/issues/1819).
- Draft stream receive window auto-tuning, preventing upper throughput limit on high bandwidth-delay-product connections (e.g. 160 Mbit/s on 50 ms connection). See [github.com/mozilla/neqo#1868](https://github.com/mozilla/neqo/pull/1868).

### Software Engineer at Protocol Labs

March 2021 - December 2023

Co-lead of the open source peer-to-peer networking library [libp2p](https://libp2p.io/) and technical lead of its [Rust implementation](https://github.com/libp2p/rust-libp2p/) with 3 direct reports and [>200 external contributors](https://github.com/libp2p/rust-libp2p/graphs/contributors).

Design, specification and implementation of network protocols.
E.g. [decentralized hole punching without the reliance on central infrastructure](https://research.protocol.ai/publications/decentralized-hole-punching/seemann2022.pdf), a [distributed hash table](https://github.com/libp2p/rust-libp2p/tree/master/protocols/kad) based on the _Kademlia_ research paper and [security handshakes and multiplexing](https://github.com/libp2p/specs/tree/master/webrtc) on top of various web protocols.

Special focus on performance.
E.g. the introduction of an [automated continuous benchmark setup](https://github.com/libp2p/test-plans/blob/master/perf/README.md) cross networks, transports and implementations as well as [multiplexer receive window auto-tuning based on bandwidth-delay-product](https://github.com/libp2p/rust-yamux/pull/176).

Facilitate networking track at conferences (e.g. [FOSDEM 2022](https://archive.fosdem.org/2022/schedule/track/network/) and [libp2p day 2022](https://web.archive.org/web/20240323083808/https://blog.ipfs.tech/2022-11-22-libp2p-day-2022-recap/)) and give [>10 peer-to-peer](https://max-inden.de/tags/talk/) related talks.

Hiring manager for the libp2p team and beyond with ~50 technical interviews.


### Software Engineer at Parity

July 2019 - February 2021

Maintaining Rust peer-to-peer networking library *libp2p* and its usage within the Blockchain framework [*Substrate*](https://github.com/paritytech/substrate/).
Worked on networking stack of the byzantine fault tolerant [consensus protocol](https://arxiv.org/pdf/2007.01560.pdf).
Filling role of hiring manager for team building automated testing infrastructure.
Shepherding (Prometheus) monitoring across the company.


### Freelance Network Engineer at SpaceNet AG

June 2019

Work on multiplexed fiber-optic setup and server migration.
Wrote [Prometheus exporter to monitor data center power modules via Modbus](https://github.com/RichiH/modbus_exporter).
Gained insight into BGP infrastructure.


### Senior Software Engineer at CoreOS / RedHat

January 2017 - May 2019

Systems engineer working on the open source monitoring project **Prometheus** and its integration with the **Kubernetes** ecosystem to monitor cloud-native Linux container infrastructures.
Designing and implementing distributed systems on top of Linux and Kubernetes orchestrator.
Presenting open source work at various IT conferences and champion the Prometheus project as a core maintainer.


### Software Engineer at Innoscale

August 2014 - December 2016

Development of a master data management web application. Involved as a back and
front end JavaScript engineer. Spearheaded the introduction of a full stack
JavaScript testing environment including a continuous integration pipeline to
improve code quality and detect errors early. Coordinated and implemented the
transformation of the UI to ReactJS, reducing side effects and improving code
reusability with a component-based approach.  Providing company wide ReactJS workshops to
accelerate the transition.


### Software Engineer / Sales Engineer at Contelligence

February - July 2014

Concept creation, development and sales of a Microsoft Office Add-on to support
compliance processes for the enterprise document management in the finance
sector. Responsible for the application software testing. Introduction of a new
human resource management framework.


### Associate System Support Analyst at DHL IT-Services

July - September 2013

Working in the IBM AS400 and Linux operation team.
Development of graphical visualization tool to analyse the operation alert
system of the IBM infrastructure. Creating regular server security reports.
Management of a database for internal license management.


### System Administrator at Heuft Systemtechnik

October - November 2009

Supporting the internal IT department in hardware
maintanance, network architecture and software distribution.


## Projects & Achievements

- Author and maintainer of [`mozilla/happy-eyeballs`](https://github.com/mozilla/happy-eyeballs), the first Rust implementation of the IETF [Happy Eyeballs v3](https://github.com/ietf-wg-happy/draft-happy-eyeballs-v3) connection-racing draft — a protocol-agnostic state machine (HTTPS/SVCB records, alt-svc, ECH retry per RFC 9849) shipped in Firefox; also contributor to the IETF draft itself (2026).

- Drive Firefox's QUIC UDP IO rewrite to a memory-safe Rust stack, raising CPU-bound throughput from < 1 Gbit/s to [4 Gbit/s](https://max-inden.de/post/fast-udp-io-in-firefox/) through multi-packet IO and [segmentation offload](https://github.com/mozilla/neqo/pull/2593) (roughly 2x from GSO alone) (2025).

- Implement [receive window auto-tuning (flow-control)](https://github.com/libp2p/rust-yamux/pull/176) in Rust Yamux multiplexer implementation based on bandwidth-delay-product, moving peak throughput from ~30 Mbit/s to 1.3 Gbit/s (2023-11-23).
  In addition [improve flow-control strategy](https://discuss.libp2p.io/t/optimizing-yamux-flow-control-sending-window-update-frames-early/843/1) measuring an additional performance increase of 25% in the wild (2021-02-11).

- Creator and maintainer of official [Prometheus Rust client library](https://github.com/prometheus/client_rust) (2022-01-16).

- Design decentralized hole punching without the reliance on central infrastructure ([paper](https://research.protocol.ai/publications/decentralized-hole-punching/seemann2022.pdf)) and [add implementation in rust-libp2p](https://github.com/libp2p/rust-libp2p/issues/2052) (2022-02-09).

- Optimize metric encoding in community [Prometheus Rust client library](https://github.com/tikv/rust-prometheus/pull/327) drastically reducing memory allocations in hot-path (2020-07-19).

- Port partially lock-free Prometheus histogram implementation to the community [Prometheus Rust client library](https://github.com/tikv/rust-prometheus/pull/314) making histogram observe calls atomic across collect calls (2020-07-14).

- Implement lookups over disjoint paths based on the extension research paper [S/Kademlia](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.68.4986&rep=rep1&type=pdf) in the [Rust libp2p Kademlia implementation](https://github.com/libp2p/rust-libp2p/pull/1473). See as well [libp2p forum post](https://discuss.libp2p.io/t/s-kademlia-lookups-over-disjoint-paths-in-rust-libp2p/571) including a summary and benchmarks. (2020-06-19)

- Kubernetes kube-state-metrics [performance optimization](https://github.com/kubernetes/kube-state-metrics/issues/498) dividing CPU usage by a factor of 6 and memory and response time by a factor of 3 through introducing an intelligent Prometheus metric cache in the code hot path and optimizing memory allocations during response generation (2019-01-11).

- Design, specification and implementation of a [new API (v2)](https://github.com/prometheus/alertmanager/pull/1352) for Prometheus Alertmanager, generated via [OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md) (2018-09-04).

- Initiate and organize distributed systems book club covering distributed and decentralized systems research and their real-world applications in [>35 sessions](https://max-inden.de/tags/distributed-systems/) (2018-08-17).

## Selected Talks & Publications

Full list at [max-inden.de/tags/talk](https://max-inden.de/tags/talk/).

- ["Fast UDP I/O for Firefox in Rust"](https://max-inden.de/post/fast-udp-io-in-firefox/) — technical write-up (2025); reached [#1 on Hacker News](https://news.ycombinator.com/item?id=45387462) and was [covered by APNIC](https://blog.apnic.net/2025/11/28/fast-udp-i-o-for-firefox-in-rust/).

- ["Happy Eyeballs v3 in Firefox"](https://youtu.be/l9eId_Yjoew) — IETF 125, Happy Eyeballs working group (2026).

- ["Modern Network Protocols — What's Next for Firefox and the Web?"](https://fosdem.org/2026/schedule/event/NKWMN9-modern_network_protocols_--_whats_next_for_firefox_and_the_web/) and ["Intro to WebTransport - the next WebSocket?!"](https://fosdem.org/2026/schedule/event/9DEU7E-intro_to_webtransport_-_the_next_websocket/) — FOSDEM 2026.

- ["Fast UDP makes QUIC quicker - optimizing Firefox's HTTP3 IO stack"](https://fosdem.org/2025/schedule/event/fosdem-2025-5449-fast-udp-makes-quic-quicker-optimizing-firefox-s-http3-io-stack/) — FOSDEM 2025.

- ["Modern networking in Firefox"](https://netstack.fm/#episode-11) — netstack.fm podcast (2025).

- "Fast UDP for Firefox" at the [Munich Internet Research Retreat (MIR³)](https://www.ce.cit.tum.de/cm/events/mir3/) 2024 & 2025, plus guest lectures on HTTP/3 & QUIC in Firefox at HPI Potsdam and TU Dresden.

- [>10 peer-to-peer talks](https://max-inden.de/tags/talk/) during the Protocol Labs tenure, including ["Hole punching in the wild"](https://fosdem.org/2023/schedule/event/network_hole_punching_in_the_wild/) (FOSDEM 2023) and facilitating the FOSDEM 2022 Network Devroom.

## Volunteer Work

- Tutor and Mentor for Refugee Family | 2018 - 2022

  Tutoring Math, Physics, English and German. Mentoring and assisting with authorities.

- Prometheus Core Member | 2017 - 2020 and 2022 - Now

  Member of the upstream core team of the open source monitoring tool _Prometheus_, developing and maintaining source code, representing the project at tech-conferences and helping adoption in user communities.

- Informationsdienst Umweltrecht e.V. | 2015 - 2021

  Administrator for the non-profit _Informationsdienst Umweltrecht e.V._ for their online presence.

- (Certified) Ski Instructor | 2017 - Now

- Student Council | 2013 -2016

  Member of the _Fachschaft WiWi_ student council, helping students of the faculty in their day-to-day student life, taking the role of the Website Administrator.

- Math, Physics and English Tutor | 2010 - 2013

## Education

**Bachelor at WWU Münster** | 2013 – 2016

Bachelor of Applied Science (B.A.Sc.) in Information systems at the
Westfälische Wilhelms-Universität Münster, combining computer science and
business administration with a special focus on enterprise applications and
architectures. Specialization during bachelor thesis on conception of
datastructure dialects and development of an application for metadata
management.


**Exchange Semester at UIA Kristiansand** | 2015

Participation in the bachelor and master program Information Systems at
Universitetet i Agder with the courses Open Source, development of a mobile
lecture support application, Hands-on-eBusiness for Entrepreneurs, development
of a both mobile and desktop web shop, IT and Management, operational and
strategic management of enterprise information technology, and Consumer
Behaviour, analysis and prediction of psychological, social and cultural
factors that affect consumer behaviour.


**Abitur at Amos Comenius Gymnasium Bonn** | 2004 - 2013


**Exchange year at Lugoff-Elgin High School SC USA** | 2010 - 2011


### Languages

- German (Mothertongue)
- English (Business fluent)




