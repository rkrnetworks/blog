---
title: "Break it here, not on the floor: what a GUI adds for command-line engineers (RKR Podcast ep 7)"
date: 2026-11-05T09:38:49Z
draft: false
description: "My engineers live in the command line. What does a picture add? An RKR engineer answers with the recorded SETU GUI demo: one port down, one cable trace of 34.6 meters, the fix tried in the synthetic twin first, and a walk that records synthetic survey readings."
tags: ["podcast", "GUI", "cable tracing", "Wi-Fi survey", "troubleshooting", "synthetic twin"]
slug: "rkr-podcast-ep07-break-it-here-not-on-the-floor"
audio: ["/audio/rkr-podcast-ep07-break-it-here-not-on-the-floor.mp3"]
audioDuration: "4:51"
cover:
  image: "/covers/rkr-podcast-ep07-break-it-here-not-on-the-floor.jpg"
  alt: "RKR Podcast, episode 7: break it here, not on the floor (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 7. YouTube ID QL7XshyIIO4.
seoTitle: "What a GUI adds for command-line network engineers (RKR Podcast ep 7)"
seoDescription: "One port down, a cable traced to its switch port, the fix tried in a synthetic twin first. A network lead asks what a picture adds to the command line."
categories: ["Podcast", "RKR SETU"]
---

"My engineers already work in the command line. What does a picture add?"

That's the question behind episode 7 of the RKR Networks Podcast. An RKR technical marketing engineer answers with a recorded RKR SETU demo of the GUI on a made-up building.

Everything discussed comes from recorded SETU demos run on made-up example sites. Both voices are synthetic text-to-speech. RKR SETU itself is pure code.

## Watch or listen

{{< youtube QL7XshyIIO4 >}}

Prefer audio? Listen to [episode 7 on Spotify](https://open.spotify.com/episode/01ugfhHZqSEQ9B73bdGEqr). Every question, with its timestamp, is in the YouTube description.

The short demo is in [yes, there's a GUI]({{< ref "yes-theres-a-gui-try-the-fix-in-the-synthetic-twin-first.md" >}}). This post goes through what the customer asked about it.

## One port down, on purpose

The demo takes port Gi1/0/2 down in the synthetic twin. The alert labels it SIMULATED. The failure card shows the switch still up and the access point (AP) on that port down.

The alert also lists its source: a MAC table flush and a spanning tree recompute. Here's what that means in plain terms:

- A switch keeps a **MAC address table**: which device sits behind which port. When a link goes down, entries learned on that port are flushed, and the switch learns them again when traffic returns.
- **Spanning tree** keeps one loop-free active path between switches. When the topology changes, it recomputes. How fast depends on the protocol version and on whether the port is set as an edge port.

When the link comes back, the demo shows "1 link(s) up" and "MAC learning resumed."

## Right-click, trace the cable

Right-click the AP and trace its cable. Cable 002 ends at Gi1/0/2, and it's 34.6 meters (114 feet) long.

Is 34.6 meters a problem? No. A copper Ethernet channel can be up to 100 meters: up to 90 meters of permanent link plus about 10 meters of patch cords. This cable is well inside that.

How does a tool know which port an AP is on? Devices can advertise who they are to the switch port they connect to, using LLDP (IEEE 802.1AB). The trace in the demo shows the result as a picture.

## Try the fix in the synthetic twin first

Resolve restores the link in the synthetic twin, and the modeled coverage turns green. Nothing on a real floor was touched.

The customer's point was fair: restoring a port you took down yourself is easy. Where rehearsal helps is a change like moving an AP to another port. You see what it touches before anyone climbs a ladder.

## A walk with synthetic survey readings

An avatar then walks the floor and records survey points over the modeled coverage. Two readings from the walk:

- -41 dBm, SNR 57 dB, channel 36 (5 GHz)
- -54 dBm, SNR 44 dB, channel 44 (5 GHz)

These are synthetic, not measured. **SNR** is signal minus the noise floor. For example, a -75 dBm signal over a -90 dBm noise floor gives 15 dB. Common guidance is at least 20 dB for data and 25 dB for voice. Both readings in the walk are well above that.

## What a picture adds

The command line answers the question you typed. A picture shows the things next to it: the AP that went dark, the cable, the floor around it. Both read the same synthetic twin. Neither replaces the other.

## What your team can do on Monday

- Pick one AP and trace its cable to a switch port from your records. Then check it on the floor.
- Record cable lengths. Anything near 100 meters deserves a look.
- Know which of your switch ports are edge ports.
- Rehearse port moves before the change window, not during it.

Related: [Wi-Fi keeps dropping: tracing the ticket to one cable]({{< ref "wifi-keeps-dropping-trace-ticket-to-one-cable.md" >}}), [trace it to one switch]({{< ref "wifi-keeps-dropping-trace-to-one-switch.md" >}}) and [a new switch becomes spanning tree root]({{< ref "new-switch-becomes-spanning-tree-root.md" >}}).

More in the [RKR Podcast page](/podcast/).

Book a demo with our team: sales@rkr-networks.com. In person or online.
