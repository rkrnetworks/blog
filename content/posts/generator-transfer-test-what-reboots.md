---
title: "Generator transfer test: which systems reboot during the gap"
date: 2026-10-29T10:00:00+05:30
description: "A monthly generator test should be uneventful. Then one closet switch reboots, and a few phones and cameras with it. A synthetic twin of a made-up site shows which loads sit outside the UPS before the next test."
tags: ["generator", "power resilience", "UPS", "facilities", "maintenance window", "synthetic twin", "RKR SETU"]
slug: "generator-transfer-test-what-reboots"
audio: ["/audio/generator-transfer-test-what-reboots.mp3"]
audioDuration: "4:21"
cover:
  image: "/covers/generator-transfer-test-what-reboots.jpg"
  alt: "Generator transfer test: which systems reboot during the gap (cover image)"
  hiddenInSingle: false
---

The generator test runs on the first Saturday of every month at 06:00. Utility power is cut on purpose, the generator starts, the transfer switch moves the building onto it, and after half an hour everything goes back. The facilities team signs the log. Usually that is the end of it.

This month, a help desk ticket followed on Monday. Several phones on the second floor had lost their settings, two cameras in the loading bay were offline, and one wiring closet switch showed an uptime of two days.

## The few seconds nobody thinks about

A generator does not take over instantly. When utility power drops, the generator needs some seconds to start and stabilize, and the transfer switch then moves the load across. Equipment on a UPS rides through that gap on battery and never notices. Equipment that is not on a UPS loses power for those seconds and restarts.

On paper, everything important is on a UPS. In practice, buildings change. A closet gets a second switch for a new floor tenant, and it is plugged into a wall outlet because the UPS was full. A small UPS in a closet reaches the end of its battery life and holds only a fraction of its original runtime. A camera power supply is moved during a refit and ends up on a circuit that is not backed by anything.

Each of these looks harmless. Together they mean a generator test is quietly also a power cycle test for a handful of devices nobody listed.

## Why the usual paperwork misses it

The electrical drawings show which circuits are on the UPS. The network inventory shows which switches power which phones and cameras. The closet UPS units have their own small records. Each is accurate on its own terms. None of them shows the chain from one camera, through a PoE switch, through a power strip, to a circuit that is or is not backed up.

So the only reliable test is the generator test itself, and by then the reboot has already happened.

## Walking the chain in a made-up building

Take an illustrative three-story office with a central UPS, a generator, and six wiring closets. The synthetic twin models the electrical path to each closet, the small UPS units in each, and the network devices and PoE loads behind them.

Running the generator transfer in the twin gives a short list. In closet 2B, one of the two switches is on a wall circuit with no backup, so it would restart, and with it every phone and camera it powers. In closet 1C, the small UPS battery has aged to the point where, at its current load, it may drop out before the generator takes over, so that closet is marginal. The other four closets ride through cleanly.

That list is enough to act on. Move the switch in 2B onto the closet UPS, and check that the UPS has room for it. Replace the batteries in 1C, or move some PoE load elsewhere. Then run the transfer again in the twin and confirm the list is empty.

## Before the next generator test

- List every closet and what powers each device in it, down to the outlet.
- Note which devices are on a UPS, which UPS, and how much runtime that UPS has at its current load.
- Include PoE loads such as phones, cameras and access points, since they depend on the switch's power.
- Treat battery age as part of the picture. A UPS that is present but tired is not the same as a healthy one.
- After the test, check device uptimes, not just whether the generator ran.
- Re-check whenever a closet gets new equipment.

A good generator test is boring. Making it boring again usually means finding a few devices that were never on the list in the first place.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
