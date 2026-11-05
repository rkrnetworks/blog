---
title: "One breaker away: questions on data center maintenance and the second fault (RKR Podcast ep 6)"
date: 2026-11-05T09:22:09Z
draft: false
description: "Tonight's work takes one busway out, and the check says nothing loses power. A network lead asks what one more breaker would do. An RKR engineer answers with a recorded SETU 1.0 demo of a made-up 1,024-GPU training hall."
tags: ["podcast", "data center", "power", "maintenance", "redundancy", "synthetic twin"]
slug: "rkr-podcast-ep06-one-breaker-away"
audio: ["/audio/rkr-podcast-ep06-one-breaker-away.mp3"]
audioDuration: "5:06"
cover:
  image: "/covers/rkr-podcast-ep06-one-breaker-away.jpg"
  alt: "RKR Podcast, episode 6: one breaker away (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 6. YouTube ID UVeUdv6-43Y.
seoTitle: "One breaker away: data center maintenance and the second fault (RKR Podcast ep 6)"
seoDescription: "Planned work uses up redundancy. A network lead asks what a second fault would do during busway maintenance in a made-up 1,024-GPU hall, and gets numbers."
categories: ["Podcast", "Data center"]
---

The maintenance check says nothing loses power tonight. Good. So what happens if one more thing fails while you're in there?

That's episode 6 of the RKR Networks Podcast. A network lead is back in the customer's chair, this time in a made-up GPU training hall. An RKR technical marketing engineer answers with a recorded RKR SETU 1.0 demo.

Everything discussed comes from recorded SETU demos run on made-up example sites. Both voices are synthetic text-to-speech. RKR SETU itself is pure code.

## Watch or listen

{{< youtube UVeUdv6-43Y >}}

Prefer audio? Listen to [episode 6 on Spotify](https://open.spotify.com/episode/3oTt1akl2RLLdHP5nnksEP). Every question, with its timestamp, is in the YouTube description.

The demo is written up step by step in [rehearse the maintenance, and the second fault]({{< ref "rehearse-maintenance-second-fault.md" >}}). This post follows the customer's questions.

## The hall

Four rows of 256 GPUs: 1,024 in total, all running one training job. Lose one GPU and the job halts. It restarts from its last checkpoint once the capacity is back.

Before the work, everything is on both power feeds: all 245 devices. IT load is 1,897.5 kW, and each of the two UPS systems sits at 43%.

## "Is tonight's work safe?"

Tonight's job is maintenance on busway C-A. The preview says:

- 0 devices lose power.
- 59 devices drop to reduced supply, meaning they now run on one feed.
- The job keeps running, 1,024 of 1,024 GPUs.

The customer then asked about headroom. The other busway, C-B, carries 469.1 kW, which is 712.7 A, or 57% of its 1,250 A rating. The busiest rack cord, TAP-C03-B1, carries 27.7 kW, 42.0 A, which is 67% of 63 A. Nothing is over or near its rating. These loads are declared design values, and some are assumed.

So the first answer is yes. But row C now runs on one side.

## One breaker away from what?

Planned work uses up redundancy. The next question is what a second fault would do while that redundancy is gone.

The second preview fails one tap-off breaker on top of the maintenance. Now 5 devices lose power: 4 servers and 1 other device. The job stops, with 32 of 1,024 GPUs out.

Neither fault takes anything down on its own. Together they do.

## The trip, and three alarms with one root

The demo then injects the trip for real, in the synthetic twin. The result matches the preview: 5 without power, 54 reduced, the job stopped.

Three alarms fire. The busway isolation is planned. The tap-off breaker failure is the fault. The job stop is the effect. SETU ties the job stop back to both together, as one root cause. That changes the question from "whose problem is this?" to "what does it touch?"

## What the stop costs

On numbers declared for this hall, not measured, the stop costs up to 938.7 GPU-hours: 1,024 GPUs times 55 minutes. While stopped, the hall idles 1,024 GPU-hours every hour.

## Options before the window

The episode doesn't pick one. It lists them:

- Take a checkpoint just before the window.
- Check the breaker that would be the second fault.
- Shorten or split the window.

After the restore, it's 0 without power and the job runs again. A one-page power report shows what lost power, the 32 GPUs out, and how it came back.

## What your team can do on Monday

- For every maintenance window, list what runs on one feed during the work.
- Ask "one breaker away from what?" before you approve it.
- Express headroom in amps against the rating, not just "it's fine."
- Put the cost of a stop in the change record, even as an estimate.

Related: [UPS on battery: what goes dark]({{< ref "ups-on-battery-what-goes-dark.md" >}}), [15 data center incidents in one synthetic twin]({{< ref "fifteen-data-center-incidents-build-run-manage.md" >}}), [PDU phase imbalance trips a rack breaker]({{< ref "pdu-phase-imbalance-trips-rack-breaker.md" >}}) and [one data center build-out, one page]({{< ref "data-center-build-out-one-team-one-page.md" >}}).

More in the [RKR Podcast page](/podcast/).

Book a demo with our team: sales@rkr-networks.com. In person or online.
