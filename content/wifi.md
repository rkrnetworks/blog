---
title: "Wi-Fi troubleshooting: why full bars can still mean bad Wi-Fi"
seoTitle: "Wi-Fi troubleshooting guide: drops, roaming, interference, 6 GHz"
description: "A practical guide to the Wi-Fi problems that survive a good coverage map: interference, sticky clients, roaming gaps, uplinks, DHCP and the switch one floor down."
seoDescription: "Wi-Fi keeps dropping, calls are choppy, scanners stall, yet the coverage map is green. A guide to the real causes, with every Wi-Fi post in one place."
url: "/wifi/"
layout: "hub"
hubCategory: "Wi-Fi"
breadcrumb: "Wi-Fi"
date: 2026-10-29
hiddenInRss: true
cover:
  image: "/images/hubs/wifi.jpg"
  alt: "Wi-Fi troubleshooting guide from RKR Networks"
---

"The Wi-Fi is bad" is the most common ticket in most offices, warehouses and campuses, and one of the hardest to close. The coverage map is green. The controller says every access point is up. The user still has a choppy call, a scanner still drops in aisle 12, a robot still pauses at the same spot. This guide explains why, and links every Wi-Fi post on the blog.

## Signal is not the same as service

Bars on a laptop measure received signal strength. A good connection needs more than that:

- **Signal quality, not just strength.** What matters is the signal compared with everything else on the channel. That is **SINR**, the signal to interference plus noise ratio. A strong signal on a crowded channel can be worse than a weaker one on a clean channel.
- **Airtime.** Wi-Fi is a shared medium. Every radio on the same channel within earshot takes turns. When dozens of radios share two channels, each one waits longer, and voice and video feel it first. See [39 radios on two channels]({{< ref "posts/wifi-interference-39-radios-two-channels.md" >}}).
- **Both directions.** The access point is usually louder than the client. A coverage map drawn from the access point's side can look fine while the client's uplink back to it is the weak half. See [four bars, seven megabits]({{< ref "posts/warehouse-scanners-four-bars-seven-megabits.md" >}}).
- **Everything behind the access point.** The access point needs power over Ethernet, a working switch port, the right VLANs, a DHCP server that answers and a path to the application. Many "Wi-Fi" problems live in the wired network.

## The usual suspects

**Channel planning and interference.** Too few channels, too much transmit power or neighbouring networks lead to co-channel contention. In the 5 GHz band, **DFS** channels can be vacated when radar is detected, which can push access points onto fewer channels without anyone changing the plan.

**Roaming.** Clients, not access points, decide when to move. Some hold on to a distant access point long after a better one is overhead: the classic **sticky client**. Fast roaming features such as **802.11r** (fast BSS transition), 802.11k and 802.11v help the client make a quicker, better choice, but they have to be supported and configured consistently. See [why laptops won't roam]({{< ref "posts/sticky-wifi-clients-wont-roam.md" >}}) and, for moving machines, [where a robot's 42 ms roaming gap comes from]({{< ref "posts/robot-wifi-roaming-42-ms-service-gap.md" >}}).

**Coverage that changes with the building.** Racking, stock levels, charging docks, glass and concrete all change how radio travels. A dead zone can appear where people rarely stand but robots always drive. See [robots stalling near the charging dock]({{< ref "posts/amr-fleet-stalls-near-charging-dock.md" >}}).

**New bands, new holes.** 6 GHz (Wi-Fi 6E and Wi-Fi 7) brings clean spectrum and wide channels, with shorter range and higher wall loss. Swapping access points one for one can leave gaps. See [moving to 6 GHz]({{< ref "posts/six-ghz-rollout-new-coverage-holes.md" >}}). Regulatory limits on **EIRP**, the effective radiated power, also differ by band and region.

**The wired side.** A floor of access points can drop together because one switch on the floor below failed, one cable went bad, or a DHCP reply is leaving the data center on the wrong link. See [Wi-Fi drops traced to one switch]({{< ref "posts/wifi-keeps-dropping-trace-to-one-switch.md" >}}) and [Wi-Fi connected with no IP address]({{< ref "posts/wifi-connected-no-ip-address-dhcp-data-hall.md" >}}).

**Segmentation.** Guest and corporate traffic are often separated with VLANs and VRFs. A shared-services change can quietly join them. See [guest Wi-Fi reaching a corporate subnet]({{< ref "posts/guest-wifi-reaches-corporate-vrf-leak.md" >}}).

## A troubleshooting order that saves time

1. **Start with the ticket, then widen.** One user, one floor or the whole site? A pattern usually points at a shared component.
2. **Check the wire before the air.** Switch, port, PoE, VLAN, DHCP. It is quicker to rule out than a channel plan.
3. **Look at quality, airtime and both directions,** not just signal strength.
4. **Ask what changed.** A firmware update, a new switch, a moved rack or a new band.
5. **Test the fix before you roll it out.** Lower power or a new channel plan helps one area and can hurt another.

## Why a synthetic twin helps

Wi-Fi problems cross teams: radio, switching, DHCP, security and facilities. A synthetic twin keeps the building, the access points, the switches, the clients and the paths between them in one model, so you can follow a ticket from the client to the cause, compare channel plans side by side, and see what a fix does to the rest of the floor before anyone climbs a ladder. The posts below each walk one problem end to end on a made-up site.

For the terms used here, see the [glossary](/glossary/). For the podcast episode on Wi-Fi that is up but not working, see the [RKR Podcast page](/podcast/).
