---
title: "Dual-homed server: both NICs up, traffic on the wrong path after a switch reboot"
date: 2026-10-29T10:00:00+05:30
description: "A server with two network connections comes through a switch reboot with both links up, yet its traffic now flows through the wrong switch and an overloaded uplink. A synthetic twin shows why, and how to keep it from happening."
tags: ["server networking", "NIC teaming", "compute", "redundancy", "switching", "synthetic twin", "RKR SETU"]
slug: "dual-homed-server-wrong-path-after-reboot"
audio: ["/audio/dual-homed-server-wrong-path-after-reboot.mp3"]
audioDuration: "3:58"
cover:
  image: "/covers/dual-homed-server-wrong-path-after-reboot.jpg"
  alt: "Dual-homed server: both NICs up, traffic on the wrong path after a switch reboot (cover image)"
  hiddenInSingle: false
---

Dual-homing a server is supposed to be the easy part of redundancy. Two network cards, two cables, two switches. If one switch goes away, traffic moves to the other. When the switch comes back, things settle down again.

Most of the time that is exactly what happens. Sometimes the switch comes back and the server keeps using the path it moved to, even though that path was meant to be the backup. Everything is up. Nothing alarms. And the backup path, which was never sized for the full load, starts to struggle.

## How a server ends up on the wrong side

Servers with two network cards usually bond them in one of a few ways. In an active-standby setup, one card carries traffic and the other waits. When the active card loses its link, the standby takes over. What happens when the original card comes back depends on a single setting: whether the server moves back to its primary, or stays where it is.

Many systems stay where they are by default, to avoid flapping back and forth. That is sensible in isolation. But in a rack where the network team assumed every server's primary card sits on switch A, it means that after any reboot of switch A, many servers end up on switch B and stay there.

Switch B's uplink was sized for half the rack's traffic, as a backup. Now it is carrying most of it.

## Why it stays hidden

Each server looks healthy. Both links are up, and the bond reports no errors. The switches are both up as well. The only sign is that one uplink is busier than usual, and that is easy to put down to growth.

And because the problem only appears after a reboot, it builds up slowly. Each maintenance window moves a few more servers across, until one day the backup uplink is close to full.

## Rebooting a switch in a made-up rack

Consider an illustrative rack of 20 servers, each with one card to switch A and one to switch B. The servers use active-standby bonding with no automatic return to the primary.

Rebooting switch A in the synthetic twin moves every server to switch B, as designed. When switch A returns, the twin shows the servers staying on switch B. Switch B's uplink now carries nearly all the rack's traffic, well beyond what it was planned for, while switch A sits almost idle.

Two alternatives can be checked right away. Setting the bonds to return to the primary card once it has been stable for a short time moves traffic back after the reboot. Switching to an active-active setup across both switches spreads the load all the time and removes the question of which side is primary. Each has its own requirements on the switch side, and the twin shows what the rack's uplinks would carry in each case, during and after the reboot.

## Things to check on dual-homed servers

- Know which bonding mode each server uses, and whether it returns to the primary after a failure.
- Size each switch's uplink for the traffic it will really carry after a failover, not just its normal share.
- After any switch reboot, check where server traffic actually settled.
- Keep bonding settings consistent across a rack, so one reboot does not leave a mix of behaviors.
- If you use active-active bonding, confirm both switches are configured to support it.
- Include servers in switch maintenance plans, not just the switches themselves.

Redundancy that only works one way is easy to miss. The failover goes fine, and the problem waits quietly for the next one.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
