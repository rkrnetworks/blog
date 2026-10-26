---
title: "Humanoids in data centers: is it possible?"
date: 2026-10-26T07:25:00Z
description: "Can a humanoid rack, stack and cable a data center? A first look at The Substrate from RKR Networks: a humanoid racks eight switches, catches its own mistakes and closes a stacking ring in a synthetic twin."
tags: ["humanoids", "physical AI", "data center robotics", "data center", "The Substrate", "synthetic twin", "RKR SETU"]
slug: "humanoids-in-data-centers-substrate-teaser"
audio: ["/audio/humanoids-in-data-centers-substrate-teaser.mp3"]
audioDuration: "3:39"
cover:
  image: "/covers/humanoids-in-data-centers-substrate-teaser.jpg"
  alt: "Humanoids in data centers: is it possible? (cover image)"
  hiddenInSingle: false
---

Can a humanoid robot cable, rack and troubleshoot a data center? We think the honest answer is: eventually, yes.

This was the first video we published, a teaser for The Substrate from RKR Networks. It shows a humanoid working a rack in a synthetic twin, seating cables and reading the network's state as it goes. This post explains what the video shows and why we think the question is worth asking now.

## Why the question matters

Hands-on data center work is precise and repetitive, and small mistakes are expensive. A cage nut that isn't seated, a cable that isn't supported by the switch it's plugged into, a ring that looks closed but isn't. Experienced technicians catch these, but they're often caught late, after the rack is handed over.

If machines are ever going to help with this work, they'll need more than strong arms. They'll need a model of the site that tells them what the right state looks like, and a way to check each step against it.

## A rack in a synthetic twin

The video below shows a new job on a made-up rack in a synthetic twin.

{{< youtube yaLDJ2HzkEI >}}

Watch it on YouTube: https://youtu.be/yaLDJ2HzkEI

A new job comes in. Rack, stack and configure eight switches in one rack, then join them as one virtual chassis, in a closed ring.

The humanoid brings the switches over on a cart and plans the work. First, the cage nuts. When one doesn't seat, it's caught and done again with a tool. Then the switches go in, one after another. Each one is lined up, seated and checked before the next, until all eight are racked.

Next, the stacking cables. The first cable goes in, and it reports a problem. It's an unsupported third-party part, so the port stays down. It's swapped for a qualified cable, and the port comes up. Cable by cable, the ring closes.

The configuration is committed and the ring is verified. All eight members are up, and with one cable down, nothing is lost.

Then the view pulls back: one rack, in one data hall. From Visakhapatnam to London and Beijing, and around the world.

## What we take from it

The interesting moments in the video aren't the ones where things go right. They're the cage nut that didn't seat and the cable that wasn't supported. In both cases the mistake was caught at the step where it happened, because each step was checked against what the rack should look like.

That's true whoever does the work. A clear plan, a check after every step, and a verification at the end are as useful to a technician today as they would be to a humanoid later. The synthetic twin is what makes those checks possible.

We're careful not to overstate where this is. It's a first look, not a finished product. But we believe it's the right direction, and we'd rather start the conversation early.

## Practical takeaways

- Break rack and stack work into steps, and check each one before the next.
- Verify parts before they go in. An unsupported cable can leave a port down while everything looks connected.
- Test resilience at handover. For a ring, that means confirming nothing is lost with one cable down.
- Keep a model of the rack's intended state. It's what turns a step list into a check list.

Can a humanoid work a data center? Eventually, yes.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
