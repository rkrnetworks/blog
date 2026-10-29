---
title: "Outages and failover: proving your network is really redundant"
seoTitle: "Network outages and failover: find single points of failure first"
description: "Why redundant networks still go down, how to find single points of failure before they find you, and every outage and failover post on the blog."
seoDescription: "Two links, two switches, two power feeds, and the site still goes dark. Learn why redundancy fails and how to find single points of failure before they bite."
url: "/outages-and-failover/"
layout: "hub"
hubCategory: "Outages and failover"
breadcrumb: "Outages and failover"
date: 2026-10-29
hiddenInRss: true
cover:
  image: "/images/hubs/outages-and-failover.jpg"
  alt: "Outages and failover guide from RKR Networks"
---

"We're fully redundant" is one of the most common things said in a first meeting about a network, and one of the least tested. Two internet links, two core switches and two power feeds look redundant on a diagram. Then one small component fails and the site goes dark anyway. This guide explains why redundancy so often fails, how to look for single points of failure, and links every outage and failover post on the blog.

## Why redundant designs still fail

**A hidden shared dependency.** Two paths are only independent if nothing important is shared. A single DNS resolver, one DHCP server, one authentication service, one patch panel or one power circuit can sit underneath both. See [a branch that loses everything when one DNS resolver fails]({{< ref "posts/branch-dns-resolver-single-point-of-failure.md" >}}).

**Failover that takes the wrong path.** Redundancy depends on the protocols choosing well when something changes. A dual-homed server can come through a switch reboot with both links up and its traffic on the wrong one. See [a dual-homed server on the wrong path]({{< ref "posts/dual-homed-server-wrong-path-after-reboot.md" >}}).

**Degraded but up.** A four-link **LACP** bundle that loses one member stays up, but hashing can put one application's flows on an overloaded link. See [one LACP member down]({{< ref "posts/lacp-member-down-uneven-hashing.md" >}}). An **OSPF** adjacency stuck in EXSTART because of an MTU mismatch leaves a backup path that never forms. See [OSPF stuck in EXSTART]({{< ref "posts/ospf-stuck-exstart-mtu-mismatch.md" >}}).

**Power behind the network.** Switches, access points and phones are only as available as the power under them. UPS runtime, which loads are actually on the UPS, and generator transfer gaps decide what stays up. See [UPS on battery: what goes dark]({{< ref "posts/ups-on-battery-what-goes-dark.md" >}}).

**The second fault.** Many designs survive one failure. Maintenance, a failed spare or an earlier fault can quietly use up the first, and the second one causes the outage. This is why **N-2** testing matters.

## Blast radius: the question to ask about every component

For each device, link and service, ask: **if this fails, who notices?** The answer is its blast radius: the hosts, access points, users, applications and sites that lose service or performance. Components with a large blast radius and no working alternative are your single points of failure.

A blast radius is more useful when it is specific. "The core switch" is not an answer. "Two floors of access points, 140 users, the voice gateway and the badge readers" is. See how one top-of-rack switch can stop a whole set of training jobs in [one ToR switch failing in a GPU cluster]({{< ref "posts/gpu-cluster-one-tor-switch-fails.md" >}}).

## A practical way to find single points of failure

1. **List the services people would call about,** such as login, Wi-Fi, phones, internet, the warehouse system and payments.
2. **Trace each one end to end:** client, access, distribution, core, WAN, DNS, DHCP, authentication, power.
3. **Fail each component in turn** and record who is affected. Then fail pairs.
4. **Rank by impact, not age.** The same method decides a refresh: replace what carries the most with the least backup. See [planning an end-of-support refresh by impact]({{< ref "posts/end-of-support-network-refresh-planning.md" >}}).
5. **Keep the list alive.** Every change and every incident should add to it or cross something off.

## From the ticket back to the cause

When an outage does happen, the quickest route to the cause is usually from the symptom inward: start at the users who called, find what they share, and follow it back. A floor of dropped Wi-Fi often leads to one switch or one cable rather than the radios. See [Wi-Fi drops traced to one switch]({{< ref "posts/wifi-keeps-dropping-trace-to-one-switch.md" >}}). Shortening that trail is what lowers **MTTR**, the mean time to repair.

## Why a synthetic twin

Testing failover on production is risky, and labs rarely match the real site. A synthetic twin lets you fail anything, including two things at once, and see the full blast radius across network, power and users, then rewind. The posts below each take one failure through on a made-up site, and the [RKR Podcast episode on proving redundancy](/podcast/) talks the idea through.

For data hall power and cooling failures, see the [data center guide](/data-center/). For changes that cause outages, see the [change rehearsal guide](/change-rehearsal/). Terms are explained in the [glossary](/glossary/).
