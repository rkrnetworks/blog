---
title: "Device up, app down: checking that a change really worked (RKR Podcast ep 4)"
date: 2026-10-29T10:15:00Z
description: "Green dashboards and unhappy users. An RKR technical marketing engineer answers with recorded SETU 1.0 demos on Wi-Fi contention, uplink, QoS and roaming. The idea running through the episode: up isn't the same as working."
tags: ["podcast", "Wi-Fi troubleshooting", "QoS", "Wi-Fi roaming", "network performance", "synthetic twin"]
slug: "rkr-podcast-ep04-its-up-is-it-working"
audio: ["/audio/rkr-podcast-ep04-its-up-is-it-working.mp3"]
audioDuration: "4:08"
cover:
  image: "/covers/rkr-podcast-ep04-its-up-is-it-working.jpg"
  alt: "RKR Podcast, episode 4: it's up. Is it working? (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 4. YouTube ID NLsGNrAwiMk.
seoTitle: "Device up, app down: checking that a change really worked (RKR Podcast ep 4)"
seoDescription: "Green dashboards, unhappy users. An RKR engineer answers with SETU 1.0 demos on Wi-Fi contention, uplink, QoS and roaming: up is not the same as working."
categories: ["Podcast", "Wi-Fi"]
---

Every link is up. Every access point is green. And the tickets keep coming: calls stall, scans time out, screen shares stutter.

That's episode 4 of the RKR Networks Podcast. A network lead is back in the customer's chair with green dashboards and unhappy users. An RKR technical marketing engineer answers with recorded SETU 1.0 demos.

Everything discussed comes from recorded SETU demos run on made-up example sites. Both voices are AI-generated.

## Watch or listen

{{< youtube NLsGNrAwiMk >}}

Prefer audio? The episode is also on the [RKR Podcast on Spotify](https://open.spotify.com/show/4uqMIzZcJCOMJ1utAEjNIJ). Every question, with its timestamp, is in the YouTube description.

## Full bars, bad calls

Signal strength says how loudly a device hears its access point. It doesn't say how much else it hears.

In the interference demo, the cause was 39 radios on two channels. Radios wait for airtime, hidden neighbours collide at the client, and the margin drops to 7 dB.

The first guess, moving the loudest neighbour, made it better but not fixed. A whole-building channel plan, with the same radios and the same power, took the margin at the first two tickets from 7 to 13 dB. 2,104 locations were rechecked, with no regressions.

Three tickets, one cause. A channel plan, not coverage.

## Four bars, seven megabits

Scanners in aisle 12 show four bars and still drop. Bars describe the downlink. The scanner's small radio, held low behind shelving, is the weaker direction.

79 of 555 spots pass on signal and fail on a usable link. Using all 8 channels moved the aisle 12 average from 25.9 to 27.9 Mbps. The worst spot was still 7 Mbps, limited by the uplink.

That's a partial result, and it's in the demo on purpose. If a synthetic twin only ever shows wins, you shouldn't trust it.

## A packet that arrives late

For a call, a late packet is a lost packet. The question isn't only whether it arrives, but whether it arrives in time.

With everything sent to the voice queue, 20 of 100 audio packets missed their deadline. With markings trusted, audio was 0 of 100, but video still missed 4 of 17. Only with video moved into the voice queue was every declared limit met, and in a real design that queue should be policed so voice keeps its guarantee. Same traffic, same moment, same network.

## A roam that worked

The radio says the robot's handover worked. The breakdown accounts for 42.05 ms of service gap, with some events still unresolved.

Each assumption was questioned one at a time. One of three changes moved nothing. The total tells you there's a problem. The breakdown tells you what to change.

## Practical takeaways

- Up isn't the same as working. Write down what good means, as a number.
- Count radios per channel, including the quiet ones.
- Measure the uplink as its own direction. Report the worst spot, not only the average.
- Test one change at a time from the same starting state.
- Make "verify connectivity" specific in every change plan.

For the written versions, read [39 radios, 2 channels]({{< ref "wifi-interference-39-radios-two-channels.md" >}}), [four Wi-Fi bars, seven megabits]({{< ref "warehouse-scanners-four-bars-seven-megabits.md" >}}), [a packet can arrive and still be late]({{< ref "qos-packet-arrives-still-late.md" >}}) and [robot Wi-Fi roaming and the 42 ms gap]({{< ref "robot-wifi-roaming-42-ms-service-gap.md" >}}).

Rehearse every change on the synthetic twin before it goes live.

More in the [RKR Podcast page](/podcast/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
