---
title: "Robot Wi-Fi roaming: where does the 42 ms service gap come from?"
date: 2026-10-26T07:30:00Z
description: "A robot moves from one access point to another and the handover works. But what did it cost? A synthetic twin accounts for a 42.05 ms gap and shows which assumptions change it and which don't."
tags: ["Wi-Fi roaming", "robotics", "AGV", "wireless design", "latency", "synthetic twin", "RKR SETU"]
slug: "robot-wifi-roaming-42-ms-service-gap"
audio: ["/audio/robot-wifi-roaming-42-ms-service-gap.mp3"]
audioDuration: "3:50"
cover:
  image: "/covers/robot-wifi-roaming-42-ms-service-gap.jpg"
  alt: "Robot Wi-Fi roaming: where does the 42 ms service gap come from? (cover image)"
  hiddenInSingle: false
---

A robot crosses from one radio to another. The radio says the handover worked. But what did it cost?

For a laptop, a short gap during a roam barely matters. For a robot moving through a warehouse, it can. A control message that arrives late, or not at all, during a handover is a real event on the floor. And when someone asks how long the gap is and why, the answer is usually a single number with no breakdown.

## Why roaming gaps are hard to reason about

A roam isn't one step. The device looks for a better access point, moves to its channel, authenticates, re-associates, completes a handshake, and the network learns where it is now. Each of those takes time, and each depends on settings and assumptions made by different people.

When the total gap is too long, the usual approach is to change something and measure again. But without knowing where the time went, it's hard to tell which change will help and which will do nothing.

## One handover in a synthetic twin

The video below follows one handover in a synthetic twin of a made-up building.

{{< youtube u4RsdVqqp6Q >}}

Watch it on YouTube: https://youtu.be/u4RsdVqqp6Q

An automated guided vehicle roams from one access point to another, and every step of the handover is recorded.

The twin computes the gap: 42.05 milliseconds accounted for, with some events still unresolved. Then it breaks down where that time went: off-channel probing, retuning to the new access point's channel, authentication, re-association, the four-frame handshake, and the round trip to the authenticator.

Then the assumptions are questioned, one at a time.

Change one assumption, and the gap changes, to 62.05 milliseconds in the video. Change another, and the world is recomputed but the result doesn't move. Change a third, and a whole delay disappears, bringing the gap down to 22.05 milliseconds.

Argue with the input, and the world recomputes.

And one more point the video makes on purpose: this building doesn't exist yet. Its network already does.

## What to take from it

Two things stand out. The first is that a breakdown is far more useful than a total. Knowing that the gap is 42.05 milliseconds tells you there's a problem. Knowing which steps make up that time tells you which setting to argue about.

The second is that not every change helps. One of the three changes in the video moved nothing at all. In production, that change would have been made, tested and left in place, and the team would have learned nothing from it. In the twin, it's clear in seconds, and the team can move on.

It also means roaming can be designed before a building is finished. If the network exists in the twin first, the robots' needs can shape the wireless design, rather than being discovered after the robots arrive.

## Practical takeaways

- Ask for a roaming gap as a breakdown, not a single number. Probing, retuning, authentication, re-association and the handshake each have their own cost.
- Write down the assumptions behind the number, and test them one at a time.
- Expect some changes to do nothing. Finding those early saves time and keeps the configuration simpler.
- For robots, design roaming against the routes they actually drive.
- Model the network before the building is finished, so wireless design can follow the work.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
