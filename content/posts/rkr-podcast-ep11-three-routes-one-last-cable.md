---
title: "Three routes, one last cable: counting redundancy all the way to the device (RKR Podcast ep 11)"
date: 2026-11-05T10:11:52Z
draft: false
description: "What really breaks when one access switch goes down? An RKR engineer answers with a recorded SETU demo of one office floor: three physical routes to the reception desk, all ending on switch two."
tags: ["podcast", "redundancy", "VLAN", "spanning tree", "change impact", "synthetic twin"]
slug: "rkr-podcast-ep11-three-routes-one-last-cable"
audio: ["/audio/rkr-podcast-ep11-three-routes-one-last-cable.mp3"]
audioDuration: "4:33"
cover:
  image: "/covers/rkr-podcast-ep11-three-routes-one-last-cable.jpg"
  alt: "RKR Podcast, episode 11: three routes, one last cable (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 11. YouTube ID 9WQQeJ-MpDQ.
seoTitle: "Three routes, one last cable: what fails when one access switch goes down (RKR Podcast ep 11)"
seoDescription: "Three physical routes to one desk, all ending on one switch. Layer by layer, what a single switch failure takes down, and how to check before you pull it."
categories: ["Podcast", "Outages and failover"]
---

"We have three routes to that desk. We're redundant."

Are you? That's episode 11 of the RKR Networks Podcast. The host asks what really breaks when one access switch on an office floor goes down. An RKR technical marketing engineer answers with one recorded RKR SETU demo: one office floor with three switches and sixteen access points.

Everything discussed comes from recorded SETU demos run on made-up example sites. Both voices are synthetic text-to-speech. RKR SETU itself is pure code.

## Watch or listen

{{< youtube 9WQQeJ-MpDQ >}}

Prefer audio? Listen to [episode 11 on Spotify](https://open.spotify.com/episode/7Bk9ES8lmfvoTo85iCQtGl). Every question, with its timestamp, is in the YouTube description. The demo itself is [on YouTube](https://youtu.be/3PWsWo84VH4).

## The floor, and one VLAN

VLAN 20 (DATA) has 20 member ports across the 3 switches. 40 cables carry it. Normally you'd answer "where does VLAN 20 go?" from a cabling spreadsheet that may or may not be current.

## One test packet

A test packet goes from the cafe device to the reception desk. It's delivered: routed across 2 routers, SW-3 then SW-1, to SW-2 port Gi2/0/21. The TTL drops from 64 to 62, because each router that forwards a packet lowers it by one.

That shows the path the packet took. It doesn't show the paths it could take.

## Three routes, one switch

A path command traces every physical route to the desk. There are three: stack link L1, stack link L2, and Trunk A then Trunk B.

All three end on switch two. The desk itself has one cable, to SW-2 Gi2/0/21. Three routes, one last switch, one last cable.

## Preview: lose switch two

The preview changes nothing. It reports, layer by layer:

- **Physical:** 52 ports and 18 cables dark.
- **Switching:** spanning tree root unchanged (SW-3), 2 ports move from blocked to forwarding, no switch isolated.
- **Routing:** 2 subnets lose their source switch: 10.30.20.0/24 (6 hosts) and 10.30.30.0/24 (4 hosts). 10 hosts unreachable.
- **Wireless:** 5 access points lose their uplink. All 22 clients on them roam. 0 stranded.

## A double failure

Lose SW-1 as well, and VLAN 20 loses its gateway. There's no first-hop redundancy standby, so hosts can't reach anything off their subnet. Now 6 clients are stranded and coverage holes appear. A Layer 2 view alone can't show this; it's a Layer 3 effect.

## Pull the power, ping, rewind

Mark "before." Pull power on SW-2. Ping 10.30.20.11: host down, destination host unreachable, 4 sent, 0 received.

Rewind to "before." The 10 hosts get their gateway back, the 5 access points recover, and the same ping gets 4 of 4 with 0% loss.

The whole test, fail, check and undo, took 31 seconds. 0 production devices were touched.

## What it didn't check

The report says it plainly: firewall policy was not checked. There's no firewall in this fabric. Nothing enforcing zone policy is not the same as nothing being blocked.

## What your team can do on Monday

- Count redundancy all the way to the device, not just to the floor.
- For each critical desk or AP, write down the last switch and the last cable.
- Check whether each VLAN's gateway has a standby.
- Read every report for what it didn't check.

Related: [Wi-Fi keeps dropping? Trace it to one switch]({{< ref "wifi-keeps-dropping-trace-to-one-switch.md" >}}), [every link up, nobody can log in]({{< ref "pruned-vlan-breaks-authentication-every-link-up.md" >}}), [swapping a floor switch at 2 AM]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}) and [fully redundant? Prove it (episode 3)]({{< ref "rkr-podcast-ep03-fully-redundant-prove-it.md" >}}).

More in the [RKR Podcast page](/podcast/).

Book a demo with our team: sales@rkr-networks.com. In person or online.
