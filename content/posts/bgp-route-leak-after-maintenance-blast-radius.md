---
title: "BGP route leak after a maintenance change: finding the blast radius"
date: 2026-10-29T10:00:00+05:30
description: "A routine maintenance change on an edge router starts announcing routes it should not. A synthetic twin of a made-up network shows who is affected, how far the leak travels and what a safer change looks like."
tags: ["BGP", "route leak", "routing", "change management", "blast radius", "synthetic twin", "RKR SETU"]
slug: "bgp-route-leak-after-maintenance-blast-radius"
audio: ["/audio/bgp-route-leak-after-maintenance-blast-radius.mp3"]
audioDuration: "4:37"
cover:
  image: "/covers/bgp-route-leak-after-maintenance-blast-radius.jpg"
  alt: "BGP route leak after a maintenance change: finding the blast radius (cover image)"
  hiddenInSingle: false
seoTitle: "BGP route leak after a maintenance change: the blast radius"
seoDescription: "An edge router change starts announcing routes it should not. See who is affected, how far the BGP leak travels and what a safer change looks like, in a twin."
categories: ["Change rehearsal", "Outages and failover"]
---

The change ticket said "replace route-map on edge router, no expected impact." Twenty minutes after the window closed, the second internet provider started carrying traffic for prefixes it had never seen before, and a partner's VPN began taking a strange path through the branch network.

Nothing was down. That is what makes a route leak so uncomfortable. Every session is established, every interface is up, and the monitoring looks green. The damage shows up as latency, as traffic in the wrong place, and sometimes as a call from an upstream provider asking why you are announcing their customer's routes back to them.

## Why route leaks are hard to see coming

A route leak is usually not one mistake. It is a filter that was edited, a policy that matched more than intended, and a neighbor that accepted what it was given. Each piece looks reasonable on its own.

The trouble is that BGP policy is spread across many devices. The route-map on one router depends on prefix lists, community tags set somewhere else, and the default behavior of the peer on the other side. To predict the effect of a change, an engineer has to hold all of that in their head, across several routers, at the same time.

Peer review helps, but the reviewer is reading the same configuration snippet as the author. Neither of them is looking at what every other router will do with the new announcements. A lab rarely has the full set of peers, and almost never has the provider side.

## Asking the question before the window

Take a made-up regional network: two data centers, 14 branch offices, two internet providers and a handful of partner connections. In a synthetic twin of that network, the planned route-map change can be applied to the edge router without touching production.

The twin then answers the questions that matter. Which prefixes would now be announced to each provider? Which of those were never meant to leave the network? Which branches would prefer a different path afterward, and by how much would their latency change? Which partner sessions would start learning routes they should not have?

In this illustrative case, the answer is that a missing match clause lets 40 internal prefixes out to the second provider, and that three branches would start sending their internet traffic through the secondary data center. That is a blast radius you can read on one page, before anyone opens a change window.

The same session can then try the corrected policy and compare the two results side by side. If the corrected version announces only what it should, and nothing else moves, the change goes ahead with a much better reason to believe "no expected impact."

## What changes in practice

The value is not that the twin knows BGP better than the engineer. It is that it applies the change to every device at once and shows the result as a list of affected prefixes, sites and paths, rather than as a feeling.

It also gives the change board something concrete. Instead of "low risk," the ticket can say which prefixes change, which sites move and which do not.

## A short checklist before touching BGP policy

- Write down the prefixes each neighbor should receive before the change, and compare against what it would receive after.
- Check outbound filters on every edge router, not just the one being changed, since a leak can enter at one point and leave at another.
- Look for community tags set on one device and matched on another. A rename on one side quietly breaks the match.
- Ask which branches or partners would change their preferred path, even if nothing goes down.
- Keep a strict outbound prefix list on every provider session that allows only your own public ranges, as a last line of defense. A maximum-prefix limit protects what you accept, not what you send.
- Rehearse the rollback, not just the change.

Route leaks are rarely dramatic in the moment. They are just expensive to clean up afterward, and almost always visible in advance if you can see the whole network at once.

Related reading: [rehearsing a route withdrawal before the window]({{< ref "one-deny-line-289-flows-rehearse-the-change.md" >}}), [a VRF route leak from guest Wi-Fi]({{< ref "guest-wifi-reaches-corporate-vrf-leak.md" >}}) and [OSPF stuck in EXSTART]({{< ref "ospf-stuck-exstart-mtu-mismatch.md" >}}). More in the [change rehearsal guide](/change-rehearsal/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
