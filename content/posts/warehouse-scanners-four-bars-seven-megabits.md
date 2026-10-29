---
title: "Four Wi-Fi bars, seven megabits: why warehouse scanners keep dropping"
date: 2026-10-26T07:20:00Z
description: "The coverage map says aisle 12 is covered, and it is. A synthetic twin walks the aisle with a handheld scanner and finds the weaker direction is the uplink, with 79 of 555 spots passing on signal but failing on usable link."
tags: ["Wi-Fi troubleshooting", "warehouse Wi-Fi", "uplink", "channel planning", "wireless design", "physical AI", "synthetic twin", "RKR SETU"]
slug: "warehouse-scanners-four-bars-seven-megabits"
audio: ["/audio/warehouse-scanners-four-bars-seven-megabits.mp3"]
audioDuration: "3:57"
cover:
  image: "/covers/warehouse-scanners-four-bars-seven-megabits.jpg"
  alt: "Four Wi-Fi bars, seven megabits: why warehouse scanners keep dropping (cover image)"
  hiddenInSingle: false
seoTitle: "Warehouse scanners keep dropping with four Wi-Fi bars: why"
seoDescription: "The coverage map says aisle 12 is covered, and it is, yet scanners keep dropping. A synthetic twin walks the aisle and finds the weaker direction is the uplink."
categories: ["Wi-Fi"]
---

A ticket comes in: scanners keep dropping in aisle 12. The coverage map says that aisle is covered. And it is. The scanner shows four bars. So why does it keep dropping?

Anyone who has supported Wi-Fi in a warehouse knows this ticket. The survey passed, the map is green, and the people on the floor still lose their connection several times a shift.

## What the bars don't show

The bars on a handheld show one thing: how well the device hears the access point. That's the downlink. But a scanner has to talk back too, and it does that with a small radio and a small antenna, usually held low, often behind shelving. The uplink, from the device back to the network, is frequently the weaker direction.

A coverage map built from the access point's side can look perfect while the uplink is struggling. Add a lot of radios sharing a few channels, and each device also gets only a slice of the airtime. None of that shows up as missing bars.

## Walking the aisle in a synthetic twin

The video below walks the aisle on a synthetic twin of a made-up warehouse network.

{{< youtube -HE2fSq6qJM >}}

Watch it on YouTube: https://youtu.be/-HE2fSq6qJM

The twin walks the aisle with Bob, who carries the scanner. His scanner shows four bars. All 62 radios in the building are active, each with a quarter of the airtime.

Bob keeps walking, and the readings follow him. Right under a radio, he gets 52 megabits. Further on, the bars still say four. Still four bars, but only 7 megabits.

The bars only show what Bob's scanner hears. The uplink, back to the radio, is the weaker direction. And 15 radios in this part of the floor share his channel.

Then Alice, in a different aisle. Same shape.

Across the floor, 79 of 555 spots pass on signal but fail on a usable link. That's the gap between what the map shows and what the scanners live with.

The store uses four channels. It has eight available. So the plan gives them all eight, with the same radios and the same power, changed in 44 places.

Aisle 12 goes from 25.9 megabits on average to 27.9. That's better, and it's honest to say it's a modest change. Bob's worst spot is still 7 megabits, and it's still the weaker direction.

## Why we show the modest result

It would be easy to stop the story at the channel change and call it fixed. We'd rather show what the twin actually found. More channels helped the aisle on average, because fewer radios share each one. But the worst spot didn't move, because the limit there is the uplink from a small handheld, not channel sharing.

That's useful to know before anyone spends a weekend re-planning the floor. It tells the team that the next step at Bob's worst spot is about the uplink itself, such as where the radios sit relative to the aisle, not about channels.

For another case where full bars hid the real cause, see [39 radios, 2 channels]({{< ref "wifi-interference-39-radios-two-channels.md" >}}).

## Practical takeaways

- Treat the uplink as its own measurement. A handheld can hear the network well and still struggle to be heard.
- Walk the route the workers walk, not just the survey grid, and record throughput along the way.
- Count how many radios share each channel, and check whether all available channels are in use.
- Look for spots that pass on signal and fail on usable link. Those are where the tickets come from.
- Be honest about partial fixes. Knowing what didn't move tells you where to look next.

Related reading: [a warehouse Wi-Fi dead zone]({{< ref "amr-fleet-stalls-near-charging-dock.md" >}}). More in the [Wi-Fi troubleshooting guide](/wifi/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
