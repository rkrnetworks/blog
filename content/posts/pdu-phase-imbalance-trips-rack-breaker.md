---
title: "One phase at 90 percent: how PDU phase imbalance trips a rack breaker"
date: 2026-10-29T10:00:00+05:30
description: "A three-phase rack PDU can look half empty and still trip a breaker if one phase carries most of the load. A synthetic twin of a made-up data hall shows where the imbalance comes from and which server move fixes it."
tags: ["PDU", "power distribution", "three-phase power", "data center", "power resilience", "synthetic twin", "RKR SETU"]
slug: "pdu-phase-imbalance-trips-rack-breaker"
audio: ["/audio/pdu-phase-imbalance-trips-rack-breaker.mp3"]
audioDuration: "4:12"
cover:
  image: "/covers/pdu-phase-imbalance-trips-rack-breaker.jpg"
  alt: "One phase at 90 percent: how PDU phase imbalance trips a rack breaker (cover image)"
  hiddenInSingle: false
seoTitle: "PDU phase imbalance: one phase at 90% trips a rack breaker"
seoDescription: "A three-phase rack PDU looks half empty and still trips a breaker when one phase carries most of the load. Find the imbalance and the server move that fixes it."
categories: ["Data center", "Outages and failover"]
---

The rack PDU reports 55 percent load. Then the other feed goes down for maintenance, and the breaker for one of its phases trips. Afterward, someone finds that phase had been running at about 90 percent while the other two were barely working.

This is one of the most common power surprises in a data hall, and it rarely comes from a single bad decision. It comes from years of small ones.

## How a rack ends up lopsided

A three-phase rack PDU splits its outlets into groups, and each group sits on one phase or one pair of phases. When a rack is first built, someone usually spreads the servers evenly. Then the rack evolves. A server is replaced with a heavier one. Two old boxes are removed from the top and a new storage shelf goes in where there was space. A network switch is plugged into whatever outlet is closest.

None of those moves look important on their own. Together, they can stack most of the load on one phase. The total rack load still looks comfortable, which is exactly why nobody goes looking.

There is a second effect that makes things worse. Servers with dual power supplies share load across both feeds. If one feed fails, the other feed's phases pick up everything. A phase at 50 percent on a normal day can be asked to carry close to double during a feed loss, and that is the moment it trips.

## Why the numbers on the PDU are not enough

Many PDUs show total load prominently and per-phase load on a second screen. Even when per-phase readings are visible, they describe today. They do not answer what happens when feed A goes away, or when the new server arriving next week is plugged in.

Answering that means knowing which server is on which outlet, which outlet is on which phase, which power supply is on which feed, and how each server's draw changes when it loses one supply. That information exists, but it is usually spread across an outlet map, a spreadsheet of server models and someone's memory.

## A worked example in a made-up hall

Consider an illustrative row of ten racks, each with a pair of three-phase PDUs on feeds A and B. In the synthetic twin, rack R6 shows a balanced-looking total. Looking per phase, phase L2 on the A-side PDU is carrying the most load in the rack.

The twin can then fail feed B. Every dual-corded server in R6 moves its full load to feed A, and phase L2 goes over its breaker rating. Phases L1 and L3 still have plenty of room. The rack did not run out of power. It ran out of one phase.

Next, the twin can move two servers from L2 outlets to L3 outlets and fail feed B again. This time all three phases stay under their limits, with a comfortable margin. That is a small physical change, two cables moved during a quiet hour, and it was found without opening the rack door.

## A quick phase-balance routine

- Record which outlet each power cord uses, and keep that map current whenever hardware changes.
- Check per-phase load, not just the rack total, and set alerts per phase.
- Ask what each phase would carry if the other feed failed, not just what it carries today.
- Place new hardware on the least-loaded phase, and check the failover case before plugging in.
- Treat network gear and other single-corded devices as their own case, since they do not share load.
- Review a few racks each quarter rather than waiting for a trip to start the review.

A breaker trip on a half-loaded rack feels unfair, but it is predictable. The information is already in the room. It just has to be put in one place and asked the right question.

Related reading: [which systems reboot in a generator test]({{< ref "generator-transfer-test-what-reboots.md" >}}), [whether one cooling failure matters]({{< ref "crac-unit-fails-is-the-room-really-n-plus-one.md" >}}) and [busway maintenance and a second fault]({{< ref "rehearse-maintenance-second-fault.md" >}}). More in the [data center guide](/data-center/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
