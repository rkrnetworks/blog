---
title: "The control link drops, the robot keeps moving: AGV failure in a synthetic twin"
date: 2026-10-26T07:45:00Z
description: "When the control uplink drops, a warehouse robot keeps driving its stored route. A synthetic twin follows both sides of the failure, the network and the physical world, from one warehouse to more than 11,000 retail sites."
tags: ["robotics", "AGV", "warehouse", "WAN resilience", "physical AI", "synthetic twin", "RKR SETU"]
slug: "agv-control-link-drops-robot-keeps-moving"
audio: ["/audio/agv-control-link-drops-robot-keeps-moving.mp3"]
audioDuration: "3:48"
cover:
  image: "/covers/agv-control-link-drops-robot-keeps-moving.jpg"
  alt: "The control link drops, the robot keeps moving: AGV failure in a synthetic twin (cover image)"
  hiddenInSingle: false
seoTitle: "AGV control link drops but the robot keeps moving: why"
seoDescription: "Warehouse robot loses its control uplink and keeps driving its stored route. Follow the network and the physical side of the failure in a synthetic twin."
categories: ["Outages and failover"]
---

The control link drops. The robot keeps moving.

That's the part of network failures in robotic sites that's easy to forget. When a link goes down in an office, work pauses. When a link goes down in a warehouse full of robots, the physical world carries on. The robot's route is stored locally, the controller's view goes stale, and the motion continues.

## Why network models need the physical side

Most network models stop at the network. They can tell you which link failed and which devices lost their path. They can't tell you what a robot was doing at the time, where it was going, or whether it reached its destination.

For a robotic site, that's only half the answer. The questions the operations team asks are physical ones. Which robots were moving? Did they stop, wait or carry on? Did the work get done, and did the system know it was done?

## Both sides of the failure in a synthetic twin

The video below follows a failure on a synthetic twin of a made-up robotic warehouse and a regional data center.

{{< youtube bZmm9KHPf4g >}}

Watch it on YouTube: https://youtu.be/bZmm9KHPf4g

The warehouse is in one model: robots, people and material flow, through receiving, storage and dispatch. The radio coverage is mapped too.

One access point loses power, and the robot hands off to the next one. A load is placed, as planned. Its route is stored on the robot itself.

Then the control uplink drops. A path is blocked, so the robot waits. The path clears, and it carries on.

Now the view zooms out, to a model of more than 11,000 retail sites. A hundred of them are checked one by one. The shared WAN path is lost, and ten sites downstream are cut off. Saved routes keep the regional data center running, and one site carries on with local route execution.

The WAN path comes back. Telemetry from the robots in the model is still stale, and local control holds. The physical motion never stops. Robot seventeen follows its committed route and reaches its destination. The link returns, and the completion comes through.

Network failures don't pause the physical world. The model shouldn't either.

## What to take from it

Two things happened at once in this failure, and the twin kept both in view. On the network side, a shared WAN path was lost and ten sites were isolated. On the physical side, robots kept moving on stored routes and finished their work, and the confirmation only arrived once the link came back.

For anyone designing or running a robotic site, that gap matters. The controller's picture is out of date for a while, even though the work is going fine. Knowing that in advance, and knowing which sites run on local routes, is very different from finding out during the outage.

For a closer look at what happens to a robot during a roam, see [where the 42 ms roaming gap comes from]({{< ref "robot-wifi-roaming-42-ms-service-gap.md" >}}).

## Practical takeaways

- Model what robots do when the control link is lost, not only the link itself.
- Know which sites and robots can run on stored routes, and for how long.
- Treat stale controller data as expected during an outage, and plan how it catches up when the link returns.
- Check shared WAN paths for the number of sites they can isolate at once.
- Test failures on both sides, network and physical, before the robots arrive.

Related reading: [AGVs that queue at one intersection]({{< ref "agvs-queue-at-one-intersection.md" >}}) and [robots stalling near the charging dock]({{< ref "amr-fleet-stalls-near-charging-dock.md" >}}). More in the [outages and failover guide](/outages-and-failover/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
