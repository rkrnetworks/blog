---
title: "Yes, there's a GUI: try the fix in the synthetic twin first"
date: 2026-11-01T12:30:00Z
draft: false
description: "A short demo of the RKR SETU GUI. A switch port goes down in a made-up office, you trace the access point to its switch port, and you try the fix in the synthetic twin before you touch the real network."
seoTitle: "Yes, there's a GUI: trace it, then try the fix in the twin"
seoDescription: "See the RKR SETU GUI: right-click an access point, trace its cable to the switch port, and rehearse the fix in a synthetic twin before touching the real network."
tags: ["network GUI", "access point", "access switch", "cable trace", "Wi-Fi survey", "change rehearsal", "synthetic twin", "RKR SETU"]
categories: ["RKR SETU", "Change rehearsal"]
keywords: ["RKR SETU GUI", "synthetic twin GUI", "trace access point to switch port", "rehearse network fix", "Wi-Fi survey points", "modelled Wi-Fi coverage", "synthetic twin", "RKR SETU"]
slug: "yes-theres-a-gui-try-the-fix-in-the-twin-first"
audio: ["/audio/yes-theres-a-gui-try-the-fix-in-the-twin-first.mp3"]
audioDuration: "2:58"
videoDuration: "PT51S"
cover:
  image: "/covers/yes-theres-a-gui-try-the-fix-in-the-twin-first.jpg"
  alt: "Yes, there's a GUI: try the fix in the synthetic twin first (cover image)"
  hiddenInSingle: false
# Video: setu_ui, RKR SETU GUI demo (0:51). YouTube ID: VIDEO_ID_SETU_UI
---

Yes, there's a GUI.

People ask us this. Many of our demos show RKR SETU from a terminal, so it's a fair question. This short demo answers it, and it shows the habit we care about most: try the change in the [synthetic twin](/glossary/#synthetic-twin) first, then touch the real network.

{{< youtube VIDEO_ID_SETU_UI >}}

Watch it on YouTube: https://youtu.be/VIDEO_ID_SETU_UI

## A port goes down

The demo runs in a synthetic twin of a made-up office. We take one switch port down on purpose. The alert says so: the port is down, and it's marked simulated.

The access point on that port goes dark with it. The failures panel shows one link down, the switch, and the access point that lost its uplink.

## Right-click and trace

You don't need to know the cabling by heart. Right-click the access point, open Topology & clients, and pick Trace to termination.

The twin draws the cable from the access point to the switch port it ends on. It's 34.6 metres of cable to one port. Now you know where to look.

## Try the fix in the twin first

The same menu has Resolve. In the demo, we click it, and the port comes back. The alert turns to restored, and the modelled coverage on the floor turns green again.

That's a rehearsal, not a repair. Nothing on a real network changed. Real fixes still need care, a change window and the people who own the kit.

What the twin gives you is a safe place to try things first. Pull the port. Restore it. Try a different order. See what the change touches before anyone walks to the closet.

Break it here, not on the floor.

## Walk the floor, record survey points

The last part of the demo walks the floor with an avatar. As it walks, it records survey points: 18 on this floor. Each point shows signal strength, signal-to-noise ratio and channel at that spot.

The colours under the walk are modelled coverage from the twin. The walk only records survey points on top.

The survey is shown as a time-lapse.

## Why it matters

Most network work isn't hard because the fix is hard. It's hard because you can't easily try it first. A synthetic twin gives you a place to experiment freely, with nothing at risk.

If you want the longer version of this idea, read [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}). For a similar ticket traced end to end, see [Wi-Fi keeps dropping? Trace it to one switch]({{< ref "wifi-keeps-dropping-trace-to-one-switch.md" >}}). And for a change rehearsed before it went live, see [one deny line, 289 flows]({{< ref "one-deny-line-289-flows-rehearse-the-change.md" >}}).

The office, the fault and every figure in the demo are made up and shown in the synthetic twin.

Book a demo with our team: sales@rkr-networks.com. In person or online.
