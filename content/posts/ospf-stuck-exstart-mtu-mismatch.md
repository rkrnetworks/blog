---
title: "OSPF stuck in EXSTART: the MTU mismatch nobody checks first"
date: 2026-10-29T10:00:00+05:30
description: "Two routers see each other, the adjacency never comes up, and the state sits in EXSTART. The cause is usually an MTU mismatch. A synthetic twin shows where the mismatch is and what else depends on that link."
tags: ["OSPF", "MTU", "routing", "troubleshooting", "synthetic twin", "RKR SETU"]
slug: "ospf-stuck-exstart-mtu-mismatch"
audio: ["/audio/ospf-stuck-exstart-mtu-mismatch.mp3"]
audioDuration: "4:20"
cover:
  image: "/covers/ospf-stuck-exstart-mtu-mismatch.jpg"
  alt: "OSPF stuck in EXSTART: the MTU mismatch nobody checks first (cover image)"
  hiddenInSingle: false
seoTitle: "OSPF stuck in EXSTART: the MTU mismatch to check first"
seoDescription: "Two routers see each other but the OSPF adjacency sits in EXSTART. It is usually an MTU mismatch. Find where, and what depends on that link, in a twin."
categories: ["Outages and failover"]
---

If you have worked with OSPF for long enough, you have seen this. Two routers on a new link, the neighbor shows up, and the state goes from INIT to 2-WAY to EXSTART and stops there. Hello packets are fine. Timers match. Areas match. The adjacency just never finishes.

Very often, the answer is MTU.

## What EXSTART is waiting for

In EXSTART, the two routers agree who leads the database exchange, and then start sending database description packets. Those packets carry the interface MTU. If one side advertises a larger MTU than the other side can accept, the receiving router drops them, and the exchange never moves on.

Hellos are small, so they pass happily. That is why the neighbor appears healthy at first glance. The failure only shows up when real data starts to move.

The mismatch usually comes from somewhere unremarkable. One end of a new link is on a port set for jumbo frames because it once carried storage traffic, while the other end uses the standard size. Or one router's interface was lowered to fit a carrier circuit or a tunnel, and the other was not. Everyone checked the obvious settings, and nobody checked this one.

## Why it causes more than a missing adjacency

A stuck adjacency is the visible symptom. The bigger question is what the network does without that link. If it was meant to be the backup path between two sites, the network looks fine today and has no backup. If it was meant to carry traffic away from a congested link, that link stays congested.

And the common workaround makes things worse. Telling OSPF to ignore the MTU lets the adjacency form, but if the MTU really is different, large packets will now be dropped on that link. The routing table looks complete while some applications start failing in ways that look nothing like a routing problem.

## Finding it in a made-up network

Picture an illustrative network with a head office, a data center and a new direct link between them, alongside an older path through a regional hub. The new link was meant to become the primary path.

In a synthetic twin of that network, the new link comes up with its configured settings. The twin shows the adjacency stuck in EXSTART, and it points at the reason: the data center router's interface is set to a jumbo MTU, while the head office router uses the standard size, which is also all the carrier handoff in the middle can carry.

It also shows the consequence. With the new link unused, traffic between the two sites keeps using the hub, and the hub's uplink sits near its limit during business hours. If the hub then failed, the head office would lose its path to the data center entirely, because the new link that should have taken over never formed an adjacency.

Fixing the MTU in the twin brings the adjacency up and shifts traffic as planned. Trying the ignore-MTU shortcut instead brings the adjacency up too, but the twin flags that packets above the carrier's limit would be dropped on the new path. Seeing both side by side makes the right fix obvious.

## Things worth checking on any new OSPF link

- Compare the interface MTU on both ends before bringing the link up, not after.
- Ask what the path in between can carry, including carrier tags, tunnels and firewalls.
- Treat ignoring the MTU as a diagnostic, not a fix.
- After the adjacency forms, check that traffic actually moved the way the design intended.
- Confirm what the network would do if the older path failed, since that is often the reason the new link exists.

EXSTART is one of those states that tells you exactly where to look, once you know what it means. The harder part is knowing what the network was quietly relying on while the link sat there doing nothing.

Related reading: [a BGP route leak after maintenance]({{< ref "bgp-route-leak-after-maintenance-blast-radius.md" >}}) and [routing and overlay faults in a data center session]({{< ref "humanoids-data-center-operations-session.md" >}}). More in the [outages and failover guide](/outages-and-failover/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
