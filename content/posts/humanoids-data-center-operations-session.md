---
title: "Can humanoids run a data center? A futuristic DC operations session"
date: 2026-10-26T07:40:00Z
description: "An eight-minute session in a synthetic twin: a humanoid racks and configures a new leaf, works through routing and overlay faults, finds a forgotten 2017 static route, and a team cleans up a dozen legacy problems."
tags: ["humanoids", "data center", "DC operations", "routing", "legacy network", "synthetic twin", "RKR SETU"]
slug: "humanoids-data-center-operations-session"
audio: ["/audio/humanoids-data-center-operations-session.mp3"]
audioDuration: "4:14"
cover:
  image: "/covers/humanoids-data-center-operations-session.jpg"
  alt: "Can humanoids run a data center? A futuristic DC operations session (cover image)"
  hiddenInSingle: false
---

Can humanoids be trained to work in a data center and manage it without human interference? That's what we're working towards at RKR Networks. This video is our longest so far: a futuristic data center operations and management session, with racking, cabling, configuration and verification, all in a synthetic twin.

## What a real day looks like

Adding a new leaf switch is rarely the hard part. The hard part is everything around it: the settings that have to match on both sides, the overlay that has to be mapped, and the legacy pieces that nobody remembers until they cause a problem. A fix someone put in years ago, a desk switch nobody owns, a router with an old setting that never got changed.

Those are the problems that take an afternoon. And they're the reason any machine doing this work would need a full model of the site, not just a task list.

## The session in a synthetic twin

The video below runs the session on a made-up network in a synthetic twin.

{{< youtube EM3CsfEmZ6E >}}

Watch it on YouTube: https://youtu.be/EM3CsfEmZ6E

A new leaf switch is racked and cabled by a humanoid. It boots, and the first configuration goes in: interfaces, routing and the overlay, one block at a time.

The first check shows the routing peers stuck, and one setting is corrected. The overlay segment is down until its mapping is added. On the second leaf, routes arrive but none are imported, so that's fixed too. A tenant route is still missing, so the tenant is tied to the overlay. Now the ping goes through, and the new cable tests clean.

Traffic moves off the old core and onto the new leaves. But one host can't be reached. Its address is claimed twice, and the trail leads to a single port.

So the whole path is diagnosed from the headquarters core. A forgotten static route from 2017 is still winning. The route is advertised properly, and the old static route is removed. Another tenant route is missing, so its route targets are fixed.

Then the team of humanoids arrives, and the legacy cleanup begins. A time server on an old switch: is it even powered? Time syncs to a new source. An old access port stuck at half duplex is set right, and the errors stop. A rogue DHCP server on an old desk is unplugged. One dark fibre strand is cleaned. An old router with a small MTU is raised to match. A desk switch sending spanning tree messages is pulled. A flapping port is set as an edge port, and the topology settles. A legacy firewall gets one new rule. An old DSL router is unplugged. And a native VLAN mismatch on an old access switch is found.

Every fault is traced, step by step, in the synthetic twin.

## What to take from it

The line we keep coming back to is from the end of the video: your change was right, and a forgotten 2017 fix broke HQ. Most of the trouble in this session didn't come from the new leaf. It came from history.

That's why we bring old and new devices into the same model. A twin that only knew about the new leaves would never have found the static route, the rogue DHCP server or the desk switch. We wrote more about that in [too old for the cloud?]({{< ref "cloud-management-for-old-and-mixed-network-devices.md" >}}).

Whether the hands are human or not, the method is the same: check every step, trace every fault, and don't assume the old network is innocent.

## Practical takeaways

- After a new switch goes in, check routing peers, overlay mapping and route imports before declaring it done.
- When a change looks right and something still breaks, look for old static routes and other forgotten fixes.
- Keep legacy devices in the model. Many of the faults in a real cleanup live on gear nobody tracks.
- Work through cleanup as a list, one fault at a time, with a check after each.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
