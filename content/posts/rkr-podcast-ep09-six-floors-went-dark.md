---
title: "Six devices lost power, six floors went dark: following one fault from the feed to the switch (RKR Podcast ep 9)"
date: 2026-11-05T10:01:43Z
draft: false
description: "At 02:10 six closets report UPS on battery. An RKR engineer answers with a recorded SETU demo of a made-up office tower: one failed rising main, found in 15 seconds, and what goes dark when the batteries run out."
tags: ["podcast", "power", "UPS", "root cause", "PoE", "synthetic twin"]
slug: "rkr-podcast-ep09-six-floors-went-dark"
audio: ["/audio/rkr-podcast-ep09-six-floors-went-dark.mp3"]
audioDuration: "4:41"
cover:
  image: "/covers/rkr-podcast-ep09-six-floors-went-dark.jpg"
  alt: "RKR Podcast, episode 9: six devices lost power, six floors went dark (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 9. YouTube ID QavTXB0nKGk.
seoTitle: "One power fault, six floors dark: count what lost power separately (RKR Podcast ep 9)"
seoDescription: "Six UPS on battery, one failed rising main. Six devices lose power, but 43 APs and 95 devices go dark. Why to count the two separately."
categories: ["Podcast", "Data center"]
---

Six devices lost power. So why did 95 devices go offline?

That's the question behind episode 9 of the RKR Networks Podcast. The host asks how one electrical fault becomes a network outage. An RKR technical marketing engineer answers with one recorded RKR SETU demo of a made-up office tower.

Everything discussed comes from recorded SETU demos run on made-up example sites. Nothing was measured. Both voices are synthetic text-to-speech. RKR SETU itself is pure code.

## Watch or listen

{{< youtube QavTXB0nKGk >}}

Prefer audio? Listen to [episode 9 on Spotify](https://open.spotify.com/episode/3PQU2dCXwkGeLghviGjJDk). Every question, with its timestamp, is in the YouTube description.

The demo is also written up in [UPS on battery: how to know what goes dark]({{< ref "ups-on-battery-what-goes-dark.md" >}}). This post follows the power path, step by step.

## The building's power, in plain terms

The declared plan: utility power plus a generator, two rising mains, a UPS in each floor closet, and 15 minutes of battery declared.

A **rising main** carries power up a tall building. Each floor taps off it. Each floor closet then runs: distribution board, floor UPS, rack PDU, switch.

The fault was set up before the recording: rising main B failed. The generator sits upstream of the riser, so it can't feed past the break.

## 02:10: six closets on battery

Six comms closets, floors 7 to 12, report UPS on battery. Closets 1 to 6 and both core UPS units are fine. Nothing is down yet.

Normally this is a flood of separate alarms, and two teams guessing. One question in SETU, "show power causes," returns one root: rising main B failed, six UPS on battery. That took 15 seconds on the demo's clock. Seven state changes were recorded under that one root.

## Follow one switch

Pick a switch on floor nine and follow its power path: one supply input, needing one. PSU, rack PDU, UPS, distribution board (no supply), riser B (failed), main switchboard, transfer switch, utility.

Any switch on those floors leads to the same failed riser. Which closet sits on which riser comes from the declared plan, so the plan needs to be right.

## What goes dark in 15 minutes

The preview, with nothing changed:

- 6 devices lose power: the 6 floor switches.
- 43 access points go off the air.
- 95 devices go offline.
- 13 clients roam.

Why so many more than six? Access points, phones and cameras usually draw power from the switch port (Power over Ethernet). When the switch goes, so do they. The demo doesn't break those out by type.

Fifteen minutes is enough to call the right closet, warn the floors and decide what matters most.

## The batteries run out

In the demo, help isn't on site in time. The model steps forward; it isn't 15 real minutes. The result matches the preview: 6 switches down, 186 links down, 43 of 85 access points off, 95 of 280 devices offline. Causes still point to the same root, now with 26 state changes.

## Restore, and what's left

Restore riser B: 0 without power, 0 of 85 access points off, 186 links back up. The one-page report shows the peak and the restore. It still lists 24 single points of failure.

## What your team can do on Monday

- Count what lost power separately from what went dark because of it.
- Write down which closet sits on which riser, and check it.
- Know how long your closet batteries really last.
- Decide now what you'd protect first with 15 minutes left.

Related: [generator transfer test: what reboots]({{< ref "generator-transfer-test-what-reboots.md" >}}), [one breaker away (episode 6)]({{< ref "rkr-podcast-ep06-one-breaker-away.md" >}}) and [rehearse the maintenance, and the second fault]({{< ref "rehearse-maintenance-second-fault.md" >}}).

More in the [RKR Podcast page](/podcast/).

Book a demo with our team: sales@rkr-networks.com. In person or online.
