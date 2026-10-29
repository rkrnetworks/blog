---
title: "One LACP member down: why the uplink looks fine but one app is slow"
date: 2026-10-29T10:00:00+05:30
description: "A four-link LACP bundle loses one member and stays up. Most traffic is fine, but one application slows to a crawl. A synthetic twin shows how hashing puts that application's flows on an overloaded link."
tags: ["LACP", "link aggregation", "switching", "load balancing", "troubleshooting", "synthetic twin", "RKR SETU"]
slug: "lacp-member-down-uneven-hashing"
audio: ["/audio/lacp-member-down-uneven-hashing.mp3"]
audioDuration: "4:08"
cover:
  image: "/covers/lacp-member-down-uneven-hashing.jpg"
  alt: "One LACP member down: why the uplink looks fine but one app is slow (cover image)"
  hiddenInSingle: false
---

Here is the support ticket in one line: "The reporting app is slow, everything else is fine." The uplink between the access switches and the core is a bundle of four links. One of them went down two days ago, the bundle stayed up on three, and the alarm was closed as non-urgent because capacity was still well above normal load.

So why is one application suffering?

## Doesn't a bundle share load evenly?

Not quite. A link aggregation bundle does not split traffic packet by packet. It assigns each flow to one member link using a hash of fields such as source and destination address, and sometimes ports. Every packet in that flow uses the same member, which keeps packets in order.

With many small flows, the hash usually spreads load fairly well. With a few large flows, it can be very uneven. Two heavy flows can land on the same member while another member sits nearly idle.

## What changes when a member goes down?

The flows that used the failed link have to be rehashed onto the remaining members. Depending on the switch, this either moves only the affected flows, or reshuffles everything. Either way, the distribution changes.

In this case, the reporting application pulls large data sets from a single database server every few minutes. Before the failure, its flows happened to share a member with light traffic. After the failure, they landed on the same member as the nightly backup that had recently been moved into business hours. That one member is now near its limit for most of the morning, while the bundle as a whole is at less than half.

## Why does monitoring show nothing wrong?

Because most dashboards watch the bundle, not its members. The bundle's total load is comfortable. The member that is struggling is visible only if someone looks at each physical interface in turn and lines up the timing with the application's complaints.

## How does the twin help?

In an illustrative office network, the synthetic twin holds the bundle, its member links, the hashing method the switches use, and the main flows that cross it. Taking one member down in the twin shows exactly the pattern described above: the bundle comfortable, one member heavily loaded, and which applications' flows are on that member.

It also makes the next steps easy to compare. Restoring the failed link brings things back to normal, of course. But the twin can also show what happens if the hash includes port numbers as well as addresses, which spreads the database flows more evenly. Or what happens if the backup is moved back to the night. Each change can be checked against the reporting application and everything else that crosses the bundle.

The more useful finding is that a member failure in this bundle is not as harmless as the alarm suggested. The network has enough total capacity, but not in the places where specific flows need it.

## What should you check on your own bundles?

- Monitor each member link, not just the bundle total.
- Know which hashing fields your switches use, and remember each end hashes its own direction independently.
- Identify the few large flows that cross each bundle, since they are the ones that hash badly.
- Treat a member failure as a capacity event for specific flows, not only a redundancy event.
- When moving scheduled jobs such as backups, check which bundles and members they will share.
- After a member is restored, confirm traffic actually rebalanced.

Link aggregation is reliable and simple, which is exactly why its uneven corners are easy to forget. When one application suffers alone, look at the member links before looking at the application.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
