---
title: "RKR Podcast, episode 2: prove I need to replace anything at all"
date: 2026-10-29T10:05:00Z
description: "A network lead argues the refresh budget with an RKR technical marketing engineer, using five SETU 1.0 demos from end of support to a failed rising main. The idea running through the episode: replace the right things first."
tags: ["podcast", "end of support", "network refresh", "lifecycle", "synthetic twin"]
slug: "rkr-podcast-ep02-replace-the-right-things-first"
audio: ["/audio/rkr-podcast-ep02-replace-the-right-things-first.mp3"]
audioDuration: "4:35"
cover:
  image: "/covers/rkr-podcast-ep02-replace-the-right-things-first.jpg"
  alt: "RKR Podcast, episode 2: prove I need to replace anything at all (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 2. YouTube ID jK4L3rbMLmc.
---

Half the switches are past end of support, and they still work. The refresh budget is on the table. The question in the room is blunt: prove I need to replace anything at all.

That's episode 2 of the RKR Networks Podcast. A network lead is back in the customer's chair. An RKR technical marketing engineer answers with five SETU 1.0 demos, from end of support to a failed rising main.

Everything discussed comes from recorded SETU demos run on made-up example sites. Both voices are AI-generated.

## Watch or listen

{{< youtube jK4L3rbMLmc >}}

Prefer audio? The episode is also on the [RKR Podcast on Spotify](https://open.spotify.com/show/4uqMIzZcJCOMJ1utAEjNIJ). Every question, with its timestamp, is in the YouTube description.

## Old, mixed, out of support

The refresh demo starts with 98 devices. 44 are past maker support, and 36 more end within 12 months.

Old or new, every device is modelled and tested the same way. Alongside the core, two other switches show the same trunk port in different command styles. Three command styles, one model.

The core is a 64-port 10G aggregation switch released in 2011. A what-if fails it on the synthetic twin, with nothing real touched. 212 guest devices would be stranded, and that's known before it fails.

The report puts the core first on the replace list, because it carries the whole tower. Refresh by impact, not by age.

## Four buckets, not two

The episode sorts the rest into keep, patch, harden or isolate, and replace. That's a planning frame, not a demo output.

Replace should be the smallest bucket, and the one with the clearest reasons. The same model with the same support date can land in a different bucket in a different building, because of what it carries.

## The access point that wasn't dead

A floor 8 Wi-Fi ticket looks like a dead access point. Replace it, and there's your refresh.

On the synthetic twin, the chain runs down to its closet and breaks in one place. Cable 137 is down, with no power reaching the access point. 8 guest devices had already roamed to neighbours, which is why tickets like this can sit.

Ticket to root cause took 63 seconds in that take, typing included. The fault was introduced into the demo before the take, so what it shows is the method.

The instruction is to test the cable first and the access point second. You spend a cable test, not a budget line.

## Six UPS alarms, one rising main

Six comms closets report their UPS on battery. From the network side, that looks like unreliable gear on six floors.

One question traces every alarm to a single failed rising main. The building's declared plan gives 15 minutes of battery. The preview shows what goes dark when it runs out: 6 switches, 43 access points and 95 devices. 13 can roam to a neighbouring access point.

It was one feed, not six floors of bad switches.

## When you do replace something

For the swap you really need, the rehearsal finds the 2 Wi-Fi devices that would be stranded, before the window rather than during it. The episode also covers backout, what the change board gets, and how presales changes when the design is tested first.

## Practical takeaways

- Don't replace by age. Replace by impact.
- Before you replace anything, find what's actually broken. Sometimes it's one cable or one power feed.
- Find what's past its security-support date, see what it carries, and fix the few that matter first.
- Keep, patch, harden or isolate, replace. A small replace bucket is a good outcome.
- Rehearse every swap before the window.

For the written version, read [end-of-support network refresh planning]({{< ref "end-of-support-network-refresh-planning.md" >}}) and [what goes dark when the UPS is on battery]({{< ref "ups-on-battery-what-goes-dark.md" >}}).

Rehearse every change on the synthetic twin before it goes live.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
