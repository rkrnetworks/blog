---
title: "Every link up, nobody can log in: how one pruned VLAN breaks authentication"
date: 2026-11-02
description: "A trunk tidy-up applies cleanly. All 141 links stay up and all 13 WAN peers stay up, yet nobody can log in. Tracing one pruned VLAN in a synthetic twin."
tags: ["VLAN", "change management", "authentication", "trunk", "root cause analysis", "synthetic twin", "RKR SETU"]
slug: "pruned-vlan-breaks-authentication-every-link-up"
audio: ["/audio/pruned-vlan-breaks-authentication-every-link-up.mp3"]
audioDuration: "4:00"
cover:
  image: "/covers/pruned-vlan-breaks-authentication-every-link-up.jpg"
  alt: "Every link up, nobody can log in: how one pruned VLAN breaks authentication (cover image)"
  hiddenInSingle: false
---

A change request comes in: tidy up a trunk. It's the kind of change nobody worries about. A few VLANs on the allowed list look unused, so they come off. The change applies cleanly, with no error and no warning. Then the calls start. Nobody can log in.

Every link is up. Every port looks the same. The wide area network hasn't moved. And yet users can't authenticate.

## Why this one is hard to see

Most of the checks we lean on during a change look at the physical layer and the obvious control plane. Are the links up? Are the ports in the right state? Are the routing peers still there? After a trunk tidy-up, all of those answers come back green.

What changed is less visible. A VLAN that was allowed on a trunk isn't any more. If that VLAN only ever carried something quiet, like the path to the authentication server, nothing in the link lights will show it. The first sign is users who can't get on the network, and by then the change is usually an hour old and nobody connects the two.

## The same change in a synthetic twin

The video below follows the change on a synthetic twin of a made-up network.

{{< youtube ZjO8gq9caKA >}}

Watch it on YouTube: https://youtu.be/ZjO8gq9caKA

The edit lands on one switch port, and its allowed VLAN list gets shorter. It applies cleanly.

Then the twin checks the network as a whole. All 141 links are still up, the 1,370 ports look the same, and all 13 WAN peers are up. On every simple measure, nothing has happened.

But the model shows the network split into two isolated islands. Every cable is up, and 13 devices are cut off.

A test frame is traced, and it's dropped at the trunk that was just tidied. VLAN 20 was pruned from the allowed list, and VLAN 20 is now split, with 2,561 paths severed. Spanning tree recounts one link, and nothing else moves.

The trunk is now asymmetric. One end still carries VLAN 20, and the other has pruned it. That's why nobody can log in. The authentication server is unreachable, because the VLAN that was pruned is the one carrying authentication.

The fix is small: put that one VLAN back on that one trunk. In the twin, the network is whole again, and login works.

## Why "everything is up" isn't enough

The lesson here isn't about VLAN pruning as such. It's that a network can be completely up and still broken. Links and ports tell you about cables and interfaces. They don't tell you whether a service can still reach the things it depends on.

The only way to know that is to check the paths, and to check them before the change goes in, not after the helpdesk fills up. In the twin, the split, the 13 isolated devices and the unreachable authentication server were all visible from the edit alone.

The same habit shows up in our post on [rehearsing a switch replacement before the maintenance window]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}).

## Practical takeaways

- Treat VLAN pruning as a real change, not housekeeping. It can remove a path without touching a single link.
- Before pruning, ask what each VLAN carries end to end, not just whether it looks busy on this trunk.
- Check both ends of a trunk. An asymmetric allowed list is easy to create and hard to spot.
- Verify services after a change, not only links. Authentication, DHCP and name resolution are good first checks.
- Keep the fix as small as the fault. Here it was one VLAN on one trunk.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
