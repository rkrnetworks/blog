---
title: "Full bars at 7, unusable at 11: one day across 20 buildings"
date: 2026-10-30T05:30:00Z
draft: false
description: "Same desk, same AP, same strong signal. At 07:00 a new laptop gets 178.7 Mbps. At 11:00 it gets 1.29 Mbps. A synthetic twin of 20 made-up buildings shows where Wi-Fi fails people, and when, every half hour."
seoTitle: "Full Wi-Fi bars at 7am, unusable at 11am: 20 buildings, every half hour"
seoDescription: "A synthetic twin of 20 made-up buildings models whether people can work at every point, every half hour. The physics, the numbers, and what to check in yours."
tags: ["Wi-Fi", "Wi-Fi troubleshooting", "wireless design", "SINR", "MCS", "airtime", "co-channel interference", "capacity planning", "video calls", "synthetic twin", "RKR SETU"]
categories: ["Wi-Fi", "RKR SETU"]
keywords: ["Wi-Fi slow at peak hours", "full bars but slow Wi-Fi", "SINR to MCS to throughput", "Wi-Fi airtime", "co-channel interference", "Wi-Fi coverage gaps by hour", "where Wi-Fi fails people", "synthetic twin", "RKR SETU"]
slug: "full-bars-at-7-unusable-at-11"
audio: ["/audio/full-bars-at-7-unusable-at-11.mp3"]
audioDuration: "11:10"
videoDuration: "PT2M39S"
cover:
  image: "/covers/full-bars-at-7-unusable-at-11.jpg"
  alt: "9,168 people. 20 buildings. Every half hour. A 3D Wi-Fi heatmap of RKR-Office-1 (cover image)"
  hiddenInSingle: false
# Video: RKR SETU 1.0 estate video (2:39). YouTube ID: P8DXkrb278s
---

It's 07:00. You sit at a desk on the sixth floor. The access point (AP) is right above you. Your new laptop gets 178.7 Mbps.

It's 11:00. Same desk. Same AP. The signal has barely moved: -35.3 dBm then, -36.3 dBm now. Full bars.

Your laptop now gets 1.29 Mbps. Not enough for a video call.

Nothing broke. The building filled up.

Our new video follows that question across a whole estate: 20 buildings, 7 building types, every half hour of one day. All 20 sites are made up. Their names start with RKR-. It's a [synthetic twin](/glossary/#synthetic-twin), not a live network. Every number below is on screen in the video.

{{< youtube P8DXkrb278s >}}

Watch it on YouTube: https://youtu.be/P8DXkrb278s

## Not a heatmap of signal

Most Wi-Fi maps answer one question: how strong is the signal here?

People care about something else: can I work here, right now?

So the demo doesn't colour each point by signal. It colours each point by the rate a new laptop would get there, at that half hour. Red means a gap. A point is a gap if either is true:

- **Signal is below -67 dBm.** This is our gap line. It's also a long-used cell-edge target for voice over Wi-Fi, from [Cisco's voice design guidance](http://www.cisco.com/en/US/docs/solutions/Enterprise/Mobility/emob30dg/Voice.html).
- **The rate is below 1.5 Mbps.** That's our line for a 1:1 video call. [Microsoft says](https://learn.microsoft.com/en-us/microsoftteams/prepare-network#bandwidth-requirements) Teams can deliver HD video in under 1.5 Mbps.

The first is a coverage problem. The second is a capacity problem. A signal map only shows the first.

## The estate at a glance

At the estate's peak, 11:00, 9,168 people are in the 20 buildings. The usable-link gap is 66,686.5 m².

By building type, in m²:

- Healthcare: 32,003.1
- Retail: 18,381.7
- Office: 9,084.7
- Education: 3,825.8
- Residential: 2,090.0
- Hospitality: 1,301.2
- Data centre: 0.0

Two sites, RKR-Education-1 and RKR-Retail-1, use a declared crowd. People over the day follow the US DOE commercial reference buildings (weekday). Crowd density for education, retail and residential follows ASHRAE 62.1.

For a CIO or CFO, this is the useful view. Not "is the Wi-Fi good?" but "where does the building fail people, and when?"

## The engineering: one desk, step by step

Here's the chain the demo shows for that sixth-floor desk at RKR-Office-1. The laptop is 1.0 m above the floor. The serving AP is on channel 165.

**1. Signal.** How much of the AP's energy reaches the laptop. Walls, floors and distance reduce it. Here it's strong all day.

**2. Interference.** Other APs on the same channel add noise. The demo sums nearby APs by their on-air share: the more an AP transmits, the more it counts. One same-channel AP is heard, at -66.0 dBm. Its on-air share rises from 3 % to 52.5 %. Interference rises from -81.2 to -68.8 dBm.

**3. SINR.** [SINR](/glossary/#sinr) compares the signal with noise plus interference. The noise floor here is -96.0 dBm. SINR falls from 45.7 dB to 32.5 dB.

**4. MCS and PHY rate.** SINR sets the modulation the radio can use (MCS). With 2 streams on 20 MHz, MCS 11 gives 287 Mbps. At 11:00 it drops to MCS 9: 229 Mbps.

**5. Throughput.** The PHY rate isn't what you get. MAC overhead and retries take a share: PHY × MAC efficiency × (1 − packet error rate). Throughput falls from 185.6 to 109.9 Mbps.

**6. Airtime.** Then the laptop has to wait its turn. [Airtime](/glossary/#airtime) is shared by every client on the AP and every radio it can hear on the channel. At 07:00, 0 clients and 96.2 % airtime left. At 11:00, 39 clients and 1.17 % left.

**7. New-laptop rate.** Throughput × airtime left. 109.9 Mbps × 1.17 % is about 1.29 Mbps.

The demo's verdict for 11:00: interference + busy cell.

The signal barely moved. The SINR still allows a fast link. The fail comes at the last step: there's almost no airtime left.

## What the numbers mean

| On screen | 07:00 | 11:00 | What it means |
|---|---|---|---|
| Signal | -35.3 dBm | -36.3 dBm | Strong. Bars look the same all day. |
| Same-channel AP on-air share | 3 % | 52.5 % | A neighbour on your channel is now busy half the time. |
| Interference | -81.2 dBm | -68.8 dBm | That neighbour's energy, weighted by how often it's on air. |
| SINR | 45.7 dB | 32.5 dB | Signal over noise plus interference. Lower means slower modulation. |
| MCS · streams · PHY | 11 · 2 · 287 Mbps | 9 · 2 · 229 Mbps | The link rate the radio picks. Still fast. |
| Throughput (MAC + retries) | 185.6 Mbps | 109.9 Mbps | What the link delivers after overhead and retries. |
| Clients on the AP | 0 | 39 | Everyone who now shares the AP. |
| Airtime left | 96.2 % | 1.17 % | How much of the channel a new laptop can still use. |
| New-laptop rate | 178.7 Mbps | 1.29 Mbps | What you actually get. Below 1.5 Mbps is a gap. |

## Three more places it fails

The video runs four deep dives. The other three are different buildings.

**RKR-Healthcare-3.** From 00:00 to 06:00, the rate at the test point drops from 24.7 Mbps to 0.

**RKR-Retail-1, self-checkout lanes.** At 00:00 the signal is -39.1 dBm and the rate is 83.3 Mbps. 13 same-channel APs already share the airtime. By 15:00 it's a busy cell.

**RKR-Hospitality-1, a guest room on F9.** From 09:00 to midnight, the signal stays at -41.6 dBm. Channel demand rises from 15 % to 133 %. Over 100 % just means demand is far above what the channel can carry. Airtime left goes from 82.7 % to 0. The rate goes from 140.8 Mbps to 0.00.

Strong signal in every case. The fail is in the airtime.

## Checking the model

A model is only useful if you can trust it. So the demo checks it.

With each building empty, we compared our signal field with the product's own coverage, point by point. 20 of 20 sites were checked. 19 matched with a max difference of 0.000 dB. The other, RKR-Office-1 F9, had a max difference of 0.078 dB across 8,677 points.

The load, the crowd and the half hours sit on top of that base.

## The compute budget

None of this needs a data centre. The video shows the budget:

- 20 sites, 48 half-hours each.
- 20,113 CPU-seconds, about 5.6 CPU-hours (labelled "CPU · 19 sites" on screen).
- About 1.5 hours elapsed, on one 16 GB machine.

Each building is solved once (12,814 CPU-s). After that, each half hour only recomputes what changed (7,299 CPU-s for the whole day). So you can ask about any site, at any half hour, on demand.

## Check your own building

These checks work on any vendor's gear.

- **Test at your busiest half hour.** A quiet-hour survey can pass while the floor fails at 11:00.
- **Look past bars.** Check SINR, MCS and channel busy at the desk, not just signal.
- **Watch airtime, not just client count.** An AP with good signal and no airtime left still fails.
- **Count radios per channel.** APs that hear each other on one channel share one queue. Review your [channel plan](/glossary/#channel-plan).
- **Test the real job.** Run a video call at a full desk. Compare what you get with 1.5 Mbps.
- **Map it by time, not just by place.** Ask where the building fails people, and when.

Want the single-office version? Watch our video on why Wi-Fi gets worse as the floor fills up: https://youtu.be/Ig0WLggOQQw. For channel plans, see [39 radios, 2 channels]({{< ref "wifi-interference-39-radios-two-channels.md" >}}) and [four bars, seven megabits]({{< ref "warehouse-scanners-four-bars-seven-megabits.md" >}}). If calls drop in one room, read [find the cause, fix it, prove it]({{< ref "video-calls-drop-meeting-room-find-fix-prove.md" >}}). New to the idea? Start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}).

## The takeaway

Signal tells you if the radio can reach you. It doesn't tell you if you can work. A synthetic twin models that, at every point, every half hour.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
