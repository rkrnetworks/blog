---
title: "Why does Wi-Fi get worse as the floor fills up?"
date: 2026-11-05T08:56:33Z
draft: false
description: "Full bars at 11:00, and the Teams call still freezes. A synthetic twin of a made-up office runs one full day and shows why: 3,411 people arrive, 10 APs share one channel, and a new device gets 1.3 Mbps."
seoTitle: "Why Wi-Fi gets worse as the office fills up"
seoDescription: "Empty at 07:00, full at 11:00. A synthetic twin of a made-up office shows how client load and co-channel interference open Wi-Fi gaps, and what to check."
tags: ["Wi-Fi troubleshooting", "wireless design", "Wi-Fi", "co-channel interference", "airtime", "client load", "5 GHz", "capacity planning", "video calls", "synthetic twin", "RKR SETU"]
categories: ["Wi-Fi", "RKR SETU"]
keywords: ["why Wi-Fi gets worse when the office is busy", "Wi-Fi slow at peak hours", "Teams call freezes full bars", "co-channel interference", "AP airtime", "PHY rate vs throughput", "Wi-Fi coverage gaps", "synthetic twin", "RKR SETU"]
slug: "why-wifi-gets-worse-as-the-floor-fills-up"
audio: ["/audio/why-wifi-gets-worse-as-the-floor-fills-up.mp3"]
audioDuration: "6:48"
videoDuration: "PT2M40S"
cover:
  image: "/covers/why-wifi-gets-worse-as-the-floor-fills-up.jpg"
  alt: "Why does Wi-Fi get worse as the floor fills up? (cover image)"
  hiddenInSingle: false
# Video: UTH Wi-Fi video (2:40). YouTube ID Ig0WLggOQQw.
---

It's 11:00. You join a Teams call from a meeting room. Your laptop shows full bars. Two minutes in, your video freezes. Then your voice goes robotic.

At 07:00, the floor was empty.

Nothing broke. No access point went down. The building just filled up.

Our new video shows why, one hour at a time. It runs a full working day, 07:00 to 19:00, on a [synthetic twin](/glossary/#synthetic-twin) of a made-up office. The office is invented. It's a rehearsal, not a live network. Every number below comes from the video.

{{< youtube Ig0WLggOQQw >}}

Watch it on YouTube: https://youtu.be/Ig0WLggOQQw

## 07:00: an empty building

Before anyone arrives, the radio already has problems. Walls and distance weaken the signal. Concrete, glass and long corridors all take their share. Far from an access point (AP), the signal is weaker before a single person walks in.

That part is the problem most people expect. A coverage survey on a quiet weekend sees it. It's real, but it isn't the whole story.

## People arrive

By 11:00, 3,411 people are in the building. They bring laptops, phones and tablets. 4,446 clients sit on 5 GHz.

People also change the radio. A body absorbs signal. A full room is a different room, as far as Wi-Fi is concerned.

## Client load: everyone takes turns

Wi-Fi is shared. On one channel, only one radio can talk at a time. Everyone else waits their turn.

That's what [airtime](/glossary/#airtime) measures. An AP's airtime is how busy the channel is, from where that AP sits. It counts its own clients. It also counts anyone else it can hear on the same channel.

At 11:00, 12 APs are at 100 % airtime. The channel is never quiet. A new device can still connect. It just rarely gets a turn.

## Co-channel interference: the neighbors are on your channel

Here's the part most people miss. In this office, 10 APs share one channel. They can hear each other, so they take turns with each other too. That's called [co-channel interference](/glossary/#co-channel-interference). Adding another AP on the same channel doesn't add capacity. It adds another radio to the queue.

At 11:00, the neighbor AP sees the channel 52 % busy.

## Full bars, 1.3 Mbps

So why does a device with a strong signal get so little?

Two numbers often get mixed up:

- **PHY rate** is how fast the radio talks while it's actually sending. It's the "link speed" your laptop shows. It depends on signal quality, the Wi-Fi generation, the number of streams and the channel width.
- **Throughput** is the data you actually get. It's what's left after taking turns, headers and acknowledgements. Throughput is always well below the PHY rate.

Bars show signal strength ([RSSI](/glossary/#rssi)). Good signal gives a high PHY rate. But a high PHY rate is no use if you rarely get to talk.

In the demo, a new device at 11:00 gets a 1.2 % share of the AP's throughput. That's 1.3 Mbps.

Microsoft's recommended bandwidth for a one-to-one Teams video call is 1.5 Mbps ([Microsoft Learn, Teams bandwidth requirements](https://learn.microsoft.com/en-us/microsoftteams/prepare-network#bandwidth-requirements)). 1.3 Mbps is under that. Full bars, frozen video.

## 11:08: the gaps peak

Across the day, the coverage gaps grow and shrink with the people. They peak at 8,933 m² at 11:08. The worst half hour is 11:00. The worst floor is F6.

Same office. Same APs. Same settings. The only thing that changed is how many people are in it.

## What caused the gaps

The video ends by splitting the gaps by cause:

- Interference × load: 50 %
- Walls + distance: 44 %
- Load: 4 %
- Bodies: 2 %

Walls and distance matter. But the biggest share comes from interference and load together: many radios on one channel, with many clients waiting to talk. That share doesn't exist at 07:00. It arrives with the people.

For an IT manager, that means a quiet-hour survey can pass and the floor can still fail at 11:00. For a CIO, it means "we need more APs" is not always the answer. More APs on the same channel can make it worse.

## What to check in your own building

These checks work on any vendor's gear.

- **Test at your busiest hour.** Survey and test when the floor is full, not when it's empty.
- **Look at channel busy, not just bars.** Check airtime on each AP at peak. An AP near 100 % has no room left.
- **Count clients per channel, not just per AP.** APs that hear each other on one channel share one queue.
- **Map which APs share a channel and can hear each other.** Review your [channel plan](/glossary/#channel-plan) and transmit power so neighbors don't overlap.
- **Test the real job.** Run a video call at a desk at peak. Compare what you get with 1.5 Mbps.
- **Find the cause before you buy.** Split coverage problems from load and interference problems. They need different fixes.
- **Rehearse the change first.** Try a new channel plan or power change in a synthetic twin. See what it does to the floor at 11:00 before you touch the real one.

Want more on this? See [39 radios, 2 channels]({{< ref "wifi-interference-39-radios-two-channels.md" >}}) and [four bars, seven megabits]({{< ref "warehouse-scanners-four-bars-seven-megabits.md" >}}). If calls drop in just one room, read [find the cause, fix it, prove it]({{< ref "video-calls-drop-meeting-room-find-fix-prove.md" >}}). New to the idea? Start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}).

## The takeaway

Bars measure signal. Calls need airtime. An office that works at 07:00 can fail at 11:00 with nothing broken. Plan for the full floor, and rehearse it before people arrive.

Book a demo with our team: sales@rkr-networks.com. In person or online.
