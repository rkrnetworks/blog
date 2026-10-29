---
title: "AGVs queue at the same intersection: is it the traffic plan or the network?"
date: 2026-10-29T10:00:00+05:30
description: "AGVs keep bunching up at one intersection on the warehouse floor. The traffic team blames the network, the network team blames the routes. A synthetic twin of a made-up warehouse separates the two."
tags: ["AGV", "robotics", "warehouse", "Wi-Fi", "traffic management", "physical AI", "synthetic twin", "RKR SETU"]
slug: "agvs-queue-at-one-intersection"
audio: ["/audio/agvs-queue-at-one-intersection.mp3"]
audioDuration: "3:37"
cover:
  image: "/covers/agvs-queue-at-one-intersection.jpg"
  alt: "AGVs queue at the same intersection: is it the traffic plan or the network? (cover image)"
  hiddenInSingle: false
seoTitle: "AGVs queue at one intersection: traffic plan or network?"
seoDescription: "AGVs keep bunching up at one warehouse intersection and each team blames the other. A synthetic twin separates the traffic plan from the network cause."
categories: ["Wi-Fi"]
---

Every afternoon, the same intersection near the outbound docks fills with AGVs. They arrive, wait, inch forward and wait again. Throughput drops and the shift lead calls it the traffic jam. The question nobody can settle is whether the AGVs are waiting for each other or waiting for the network.

Both answers are plausible, and they lead to very different fixes.

## Two ways to get a queue

An AGV waits at an intersection when its traffic manager has not yet granted it permission to cross. That can happen because another AGV is already using the space, which is a traffic problem. Or because the permission message is late, or the AGV's position update has not arrived, which is a network problem. From the floor, both look the same: a vehicle sitting still.

Traffic problems tend to grow with volume. More vehicles at peak means more waiting. Network problems tend to follow location and conditions. A weak spot near metal doors, a busy access point at shift change, a roam that happens right at the decision point.

The afternoon peak makes things harder to read, because it is when both traffic and network load are highest.

## Why the logs do not settle it

The fleet system records where AGVs waited and for how long. The wireless system records which access point each vehicle was connected to and how good the link was. Neither shows the other's view. Lining them up by time is possible, but slow, and the result is usually still open to interpretation.

## Separating the causes in a made-up warehouse

In an illustrative warehouse, the synthetic twin holds the floor layout, the AGV routes and traffic rules, the access points, and the vehicles' radio behavior. It can run the afternoon peak twice: once with a perfect network, and once with the network as designed.

With a perfect network, the intersection still sees some queuing at peak, but short and evenly spread. With the network as designed, queuing roughly doubles. The difference comes from one spot: the decision point before the intersection sits near the edge of two access points, and vehicles often roam right there. During the roam, their position updates arrive late, the traffic manager holds them, and the vehicles behind them stack up.

So the answer is both, and the twin shows how much each contributes. Moving the decision point a couple of meters earlier, into stronger coverage, removes most of the extra waiting. Adjusting the traffic rule for that intersection handles what remains.

## When AGVs keep queuing in one place

- Compare queue times at peak with and without network effects before changing anything.
- Check where vehicles roam relative to decision points and intersections.
- Avoid placing decision points at the edge between two access points.
- Look at access point load at shift change, when people and vehicles share the air.
- Review traffic rules for intersections that see heavy cross traffic.
- After any change, measure queue times at the same hour, not across the day.

Robots that wait are telling you something. The hard part is working out whether they are waiting for each other or for the network.

Related reading: [a dead zone near the charging docks]({{< ref "amr-fleet-stalls-near-charging-dock.md" >}}), [robot Wi-Fi roaming gaps]({{< ref "robot-wifi-roaming-42-ms-service-gap.md" >}}) and [what an AGV does when its control link drops]({{< ref "agv-control-link-drops-robot-keeps-moving.md" >}}). More in the [Wi-Fi troubleshooting guide](/wifi/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
