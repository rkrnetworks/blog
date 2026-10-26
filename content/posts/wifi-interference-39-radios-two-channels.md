---
title: "39 radios, 2 channels: when full Wi-Fi bars still mean bad calls"
date: 2026-10-26T06:50:00Z
description: "Three tickets on three floors, all with full bars. In a synthetic twin, the cause turns out to be the channel plan, not coverage: 39 radios sharing two channels."
tags: ["Wi-Fi troubleshooting", "channel planning", "interference", "SINR", "wireless design", "synthetic twin", "RKR SETU"]
slug: "wifi-interference-39-radios-two-channels"
audio: ["/audio/wifi-interference-39-radios-two-channels.mp3"]
audioDuration: "4:16"
cover:
  image: "/covers/wifi-interference-39-radios-two-channels.jpg"
  alt: "39 radios, 2 channels: when full Wi-Fi bars still mean bad calls (cover image)"
  hiddenInSingle: false
---

A ticket comes in: video calls keep stalling in my room, and the Wi-Fi shows full bars. A second one follows from one floor up, at the same end of the hall: scans keep timing out. Then a third, from the ground floor: screen share keeps stuttering.

Three tickets, three floors, and every one of them says the signal is fine. They're right. That's what makes this kind of problem slow to solve.

## Why full bars can mislead

Signal strength tells you how loudly a device hears its access point. It doesn't tell you how much else it hears at the same time. In a busy building, the problem is often not too little signal but too many radios sharing too few channels.

Two things happen when that's the case. Neighbours on the same channel raise the noise floor, so the margin between the wanted signal and everything else shrinks, and the client drops to a slower rate. And every neighbour a radio can hear is one it has to wait for before it sends, so the airtime gets shared out between them. Neither shows up as missing bars.

## Three tickets in a synthetic twin

The video below works the tickets on a synthetic twin of a made-up four-floor building.

{{< youtube _q2lvVvhebs >}}

Watch it on YouTube: https://youtu.be/_q2lvVvhebs

At both of the first two tickets, the signal is strong, well above the real-time target. Coverage looks fine. Signal was never the question.

So the twin measures the signal against the noise floor beneath it. At the same spot, with neighbours transmitting, that margin shrinks to 7 decibels. The neighbours lift the noise floor by 57 decibels, and at that margin the client drops to its slowest rate.

The tickets line up, floor over floor. The loudest neighbour on the same channel is 18 metres down the hall. Twelve more sit below the level this radio listens for, hidden from it. Every neighbour the radio does hear, it waits for before it sends, so here the channel is shared six ways.

Then the plan itself: 39 radios on two channels.

The first guess is the obvious one. Move the loudest neighbour off the channel, at the same power. The margin improves from 7 to 11 decibels. Better, not fixed. One floor up, it barely moved.

The cause was never one radio. It's the plan. So the plan is redrawn with four channels, at the same power and the same access point locations. The fix is distance, against both kinds of neighbour: the ones a radio hears, and the hidden ones.

At the first two tickets, the margin goes from 7 to 13 decibels. On the ground floor it goes from 10 to 42 decibels. And 2,104 locations across the building are rechecked, with no regressions.

Three tickets, one cause. The channel plan, not coverage.

## Why the first guess wasn't enough

Moving one noisy radio is the fix most of us would try first, and it did help. But it treated a design problem as a local one. Testing the guess in the twin before touching production showed that quickly: better at one spot, barely changed one floor up.

Changing the plan, and then rechecking the whole building, is what turned three separate tickets into one answer. It's the same idea behind our post on [tracing a Wi-Fi ticket to one cable]({{< ref "wifi-keeps-dropping-trace-ticket-to-one-cable.md" >}}): follow the cause, not the symptom.

## Practical takeaways

- When users have full bars and poor performance, look at signal over noise, not signal alone.
- Count how many radios share each channel, including the ones too quiet for a radio to hear.
- Line tickets up by location. Problems stacked floor over floor often share a cause.
- Test a fix against the whole building, not just the spot in the ticket, and check for regressions.
- Sometimes the fix is the plan, not the hardware. Same radios, same power, more channels.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
