---
title: "Unplug, replug, trace, clean: 11 everyday network jobs done by a humanoid robot in a synthetic twin"
date: 2026-11-05T10:21:57Z
draft: false
description: "A roundup of our humanoid Shorts: a robot racks a switch, replugs a port, swaps a bad cable, cleans a fiber, and hunts down a rogue DHCP server, a rogue switch and a rogue DSL router. All in RKR SETU, a synthetic twin of a whole estate."
tags: ["humanoid robots", "troubleshooting", "data center", "Layer 1", "synthetic twin"]
slug: "everyday-network-jobs-done-by-a-humanoid-robot"
audio: ["/audio/everyday-network-jobs-done-by-a-humanoid-robot.mp3"]
audioDuration: "4:33"
cover:
  image: "/covers/everyday-network-jobs-done-by-a-humanoid-robot.jpg"
  alt: "Eleven everyday network jobs, done by a humanoid robot in a synthetic twin (cover image)"
  hiddenInSingle: false
# Shorts: bu7hJYOMBrA J4iH3IHkeKw OfeRfsZRUv4 qNcUZKHRshU FAEZiiUs0MU R_2WnLcOKDU VmhUDNQccv4 9ecIGShi16w lmQDFjnFg6Y DAIAqfRWppM UaHZ0Itig2I
seoTitle: "11 everyday network jobs, done by a humanoid robot in a synthetic twin"
seoDescription: "Unplug and replug, a bad cable pair, a dirty fiber, rogue DHCP, a rogue switch, a legacy firewall blocking VXLAN. Short clips from RKR SETU, with what each one teaches."
categories: ["Data center"]
---

Most tickets aren't exotic. A cable isn't plugged in. A port needs a replug. Someone brought a box from home and plugged it into the wall.

Over the last two weeks we posted a series of YouTube Shorts in which a humanoid robot does these everyday jobs inside RKR SETU, a synthetic twin of a whole estate: network, Wi-Fi, security, compute, power and cooling. Each clip is under a minute. Here they are in one place, with what each one teaches.

These are demos in a synthetic twin, not a live site. For the longer session, see [can humanoids run a data center?]({{< ref "humanoids-data-center-operations-session.md" >}})

## 1. Rack, cable, configure

A humanoid operator racks a switch, cables it, and rolls up to start configuring.

{{< youtube bu7hJYOMBrA >}}

## 2. The oldest trick in IT

The port shows notconnect. Unplug, replug, and it comes up connected. The basics still matter.

{{< youtube J4iH3IHkeKw >}}

## 3. When it's actually Layer 1

A cable test flags an impedance mismatch on pair D. Swap the cable, retest, and it's normal. An Ethernet cable has four twisted pairs, A to D. One bad pair can be enough to cause errors or a slower link.

{{< youtube OfeRfsZRUv4 >}}

## 4. Badge in, badge out

Physical access is modeled too. The team badges through the door, the reader turns green, and they're in.

{{< youtube qNcUZKHRshU >}}

## 5. A 2017 fix that broke HQ

A static route labeled TEMP-FIX-2017 was still steering an HQ prefix toward a dead next hop, and BGP had no route for it. One path check showed it. The fix: advertise the prefix and remove the static route. Temporary fixes need an end date.

{{< youtube FAEZiiUs0MU >}}

## 6. The switch that was never plugged in

NTP won't sync. Check the physical switch: there's no power cord in the inlet. Plug it in, and it syncs. Check power before you check config.

{{< youtube R_2WnLcOKDU >}}

## 7. Hunting a rogue DHCP server

Clients get DHCP offers from the wrong place. They trace back to an unmanaged gateway box on an old desk. Unplug it, and the problem is gone. (General advice, not shown in this Short: enable DHCP snooping with access ports untrusted and uplinks / the real DHCP server port trusted; use the binding table, and consider rate limits. Often paired with dynamic ARP inspection and IP source guard.)

{{< youtube VmhUDNQccv4 >}}

## 8. Fiber hygiene

Receive power drops to -31 dBm. Clean the fiber port with a click pen, and it jumps back to -3.4 dBm. A dirty connector is one of the most common optical faults, and the cheapest to fix.

{{< youtube 9ecIGShi16w >}}

## 9. Who plugged a switch into the wall port?

A port goes err-disabled from BPDUs. The source is a consumer 8-port switch on an old desk. BPDU guard did its job: an access port that sees spanning tree frames shuts itself down. Pull the uplink, done.

{{< youtube lmQDFjnFg6Y >}}

## 10. When a legacy firewall ruins your overlay

The overlay keeps dropping. The real cause is an old firewall rule blocking VXLAN (UDP port 4789) between the VTEPs, the devices that wrap and unwrap overlay traffic. Add a permit rule, and the overlay comes back.

{{< youtube DAIAqfRWppM >}}

## 11. Taking down a rogue DSL router

A duplicate ARP is traced to an old DSL router on a desk. Unplug its LAN cable, and the traffic settles.

{{< youtube UaHZ0Itig2I >}}

## What these have in common

- Check Layer 1 first: power, cable, connector.
- Unmanaged boxes on desks cause real outages. Protect access ports.
- Old rules and temporary routes outlive the reason they were added.
- A synthetic twin lets you practice the walk from symptom to cause before it happens for real.

Related: [humanoids in data centers: is it possible?]({{< ref "humanoids-in-data-centers-substrate-teaser.md" >}}), [humanoid robots, aisle width and cable trays]({{< ref "humanoid-robots-aisle-width-cable-trays.md" >}}) and [Wi-Fi connected, no IP address]({{< ref "wifi-connected-no-ip-address-dhcp-data-hall.md" >}}).

Book a demo with our team: sales@rkr-networks.com. In person or online.
