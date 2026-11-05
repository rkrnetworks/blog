---
title: "Fine at seven, unusable at eleven: a customer's questions on Wi-Fi by the hour (RKR Podcast ep 8)"
date: 2026-11-05T09:51:38Z
draft: false
description: "The Wi-Fi was fine this morning, and by lunch nobody can join a call. An RKR engineer answers with a recorded SETU demo of 20 made-up buildings, checked every half hour: an office desk, a hospital, self-checkout lanes and a hotel room, each failing at its own hour."
tags: ["podcast", "Wi-Fi troubleshooting", "airtime", "capacity planning", "co-channel interference", "synthetic twin"]
slug: "rkr-podcast-ep08-when-the-building-fails-people"
audio: ["/audio/rkr-podcast-ep08-when-the-building-fails-people.mp3"]
audioDuration: "5:22"
cover:
  image: "/covers/rkr-podcast-ep08-when-the-building-fails-people.jpg"
  alt: "RKR Podcast, episode 8: full bars at seven, unusable at eleven (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 8. YouTube ID HgO3CT5f5TI.
seoTitle: "Why Wi-Fi fails at different hours in different buildings (RKR Podcast ep 8)"
seoDescription: "Office at 11:00, hospital at 06:00, shop at 15:00, hotel at midnight. Strong signal every time; the failure is airtime. Map Wi-Fi by time, not just place."
categories: ["Podcast", "Wi-Fi"]
---

"The Wi-Fi was fine this morning. By lunch, nobody can join a call."

That's the complaint behind episode 8 of the RKR Networks Podcast. An RKR technical marketing engineer answers with a recorded RKR SETU demo of a test estate: 20 made-up buildings of 7 types, checked every half hour.

Everything discussed comes from recorded SETU demos run on made-up example sites. Every reading is modeled. Both voices are synthetic text-to-speech. RKR SETU itself is pure code.

## Watch or listen

{{< youtube HgO3CT5f5TI >}}

Prefer audio? Listen to [episode 8 on Spotify](https://open.spotify.com/episode/6HqvVleEkdd3ePtdNI0v1H). Every question, with its timestamp, is in the YouTube description.

The office desk and the estate totals are written up in [full bars at 7, unusable at 11]({{< ref "full-bars-at-7-unusable-at-11.md" >}}). This post adds the three other buildings from the episode, and the questions.

## What counts as a gap

The demo marks a spot as a gap if the signal is below -67 dBm, or if a new laptop would get less than 1.5 Mbps. -67 dBm is a long-used cell-edge target for voice. 1.5 Mbps is about what a one-to-one video call needs.

The second test is the one most maps skip. A signal map shows coverage. It doesn't show capacity.

## The office desk: signal flat, rate collapses

At one office desk, signal barely moves: -35.3 dBm at 07:00, -36.3 dBm at 11:00. What a new laptop can get falls from 178.7 Mbps to 1.29 Mbps.

Why? One same-channel neighbor AP gets busy as people arrive. Its time on air goes from 3% to 52.5%. The serving AP's clients go from 0 to 39, and its airtime left drops from 96.2% to 1.17%.

**Airtime** is the share of time the channel is free for you to talk. Radios on one channel take turns. A strong signal doesn't help if you rarely get a turn.

## The hospital at 06:00

A hospital point near a phone, on channel 52. Signal: -35.6 dBm at midnight, -36.6 dBm at 06:00. But 7 same-channel APs share the airtime, and channel demand rises from 59.2% to 148%.

Over 100% means the devices want far more time than the channel has. The verdict at 06:00: interference plus a busy cell.

## Self-checkout lanes at 15:00

A shop's self-checkout lanes on channel 36. Signal is -39.1 dBm both times. At midnight, a new device gets 83.3 Mbps. At 15:00, 33 clients push demand to 752%, airtime left is 0, and the rate is 0.00 Mbps. The verdict: busy cell from load.

## A hotel room at midnight

A hotel guest room on channel 44. Signal is -41.6 dBm both times. At 09:00, the rate is 140.8 Mbps. At midnight, neighboring rooms are streaming. Demand reaches 133%, airtime left is 0%, and the rate is 0.00 Mbps.

## Strong signal every time

In all four places, the signal was strong. The failure was in the airtime.

Across the estate, the gap area peaks at 11:00: 66,686.5 square meters, with 9,168 people in the buildings. At midnight it's 35,406.9 square meters. But not every type peaks at 11:00. The hotels are worst at midnight. There's no single busy hour.

## What your team can do on Monday

- Find each building's busiest half hour, and test then.
- A quiet-hour survey can pass and the floor can still fail.
- Look at airtime, not just client count.
- Remember that radios on one channel share one queue.
- Test the real job, such as a video call, not just bars.
- Map it by time, not just by place.

The film shows no fix being tried. If you change a channel plan, rehearse it first.

Related: [why Wi-Fi gets worse as the floor fills up]({{< ref "why-wifi-gets-worse-as-the-floor-fills-up.md" >}}), [39 radios, 2 channels]({{< ref "wifi-interference-39-radios-two-channels.md" >}}) and [video calls drop in one meeting room]({{< ref "video-calls-drop-meeting-room-find-fix-prove.md" >}}).

More in the [RKR Podcast page](/podcast/).

Book a demo with our team: sales@rkr-networks.com. In person or online.
