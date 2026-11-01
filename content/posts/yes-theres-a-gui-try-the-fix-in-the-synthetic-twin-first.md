---
title: "Yes, there's a GUI: try the fix in the synthetic twin first"
date: 2026-11-01T12:30:00Z
draft: false
description: "The RKR SETU GUI in 50 seconds: a 3D synthetic twin of a multi-floor building, a simulated switch-port failure, the access point's cable traced to its exact switch port with length, the fix rehearsed in the synthetic twin, and a survey walk over modelled Wi-Fi coverage."
seoTitle: "Yes, there's a GUI: trace it, then try the fix in the synthetic twin"
seoDescription: "See the RKR SETU GUI: a 3D synthetic twin of a multi-floor building. Inject a port failure, trace the AP's cable to its exact switch port with length, and rehearse the fix in the synthetic twin first."
tags: ["network GUI", "access point", "access switch", "cable trace", "Wi-Fi survey", "Wi-Fi coverage", "change rehearsal", "synthetic twin", "RKR SETU"]
categories: ["RKR SETU", "Change rehearsal"]
keywords: ["RKR SETU GUI", "synthetic twin GUI", "3D synthetic twin", "trace access point to switch port", "cable length", "failure injection", "rehearse network fix", "Wi-Fi survey points", "modelled Wi-Fi coverage", "synthetic twin", "RKR SETU"]
slug: "yes-theres-a-gui-try-the-fix-in-the-synthetic-twin-first"
audio: ["/audio/yes-theres-a-gui-try-the-fix-in-the-synthetic-twin-first.mp3"]
audioDuration: "3:29"
videoDuration: "PT51S"
cover:
  image: "/covers/yes-theres-a-gui-try-the-fix-in-the-synthetic-twin-first.jpg"
  alt: "Yes, there's a GUI: try the fix in the synthetic twin first (cover image)"
  hiddenInSingle: false
# Video: setu_ui, RKR SETU GUI demo (0:51). YouTube ID: 6hD3JO2_Je0
---

Yes, there's a GUI.

And there's a lot behind it. In 50 seconds, this demo shows RKR SETU's [synthetic twin](/glossary/#synthetic-twin) of a whole multi-floor building in 3D: every floor, every access point, every cable from the access point to its switch port. Then it breaks something on purpose, traces it, and rehearses the fix in the synthetic twin first.

{{< youtube 6hD3JO2_Je0 >}}

Watch it on YouTube: https://youtu.be/6hD3JO2_Je0

## Inject a failure

We take one switch port down in the synthetic twin. The alert names it straight away: port CLS-SW-1 Gi1/0/2 is down, marked simulated, with the cause beside it: MAC table flush and STP recompute.

The access point on that port goes dark with it. The failures panel shows the link that's down, the switch and port, the access point that lost its uplink, and the cable behind it: Cable 002, 34.6 metres, 114 feet.

## Trace the cable to its exact switch port

Right-click the access point, open Topology & clients, and pick Trace to termination.

The synthetic twin draws Cable 002 through the building, from CLS-F1-AP-02 to the exact port it terminates on: CLS-SW-1 Gi1/0/2, 34.6 metres, 114 feet. The same menu shows the AP chain from switch to wireless controller, the clients on the access point, and the blast radius: what fails with it.

## Try the fix in the synthetic twin first

The same menu has Resolve. Click it, and the port comes back: the alert reads restored, simulated, MAC learning resumes, and the modelled coverage on the floor turns green again.

That's the point of rehearsing in the synthetic twin. Pull the port. Restore it. Try a different order. See exactly what the change touches before anyone walks to the closet, and take a fix you've already rehearsed to the real network.

Break it here, not on the floor.

## Walk the floor, record survey points

The last part of the demo walks the floor with an avatar, recording survey points as it goes: 18 on this floor. Each point carries signal strength, signal-to-noise ratio and channel at that spot.

Under the walk is modelled Wi-Fi coverage, floor by floor, computed by the synthetic twin. The walk records the survey points on top of it.

## Why it matters

Most network work isn't hard because the fix is hard. It's hard because you can't easily try it first. A synthetic twin of your building, with every cable traced to its port and coverage modelled per floor, gives you that place. Experiment safely there, then touch the real network.

If you want the longer version of this idea, read [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}). For a similar ticket traced end to end, see [Wi-Fi keeps dropping? Trace it to one switch]({{< ref "wifi-keeps-dropping-trace-to-one-switch.md" >}}). And for a change rehearsed before it went live, see [one deny line, 289 flows]({{< ref "one-deny-line-289-flows-rehearse-the-change.md" >}}).

Fault introduced in the synthetic twin for this demo. Survey sped up and edited for length.

Book a demo with our team: sales@rkr-networks.com. In person or online.
