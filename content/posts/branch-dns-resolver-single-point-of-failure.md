---
title: "When one DNS resolver goes, the branch goes: finding hidden dependencies"
date: 2026-10-29T10:00:00+05:30
description: "A branch office with two internet links and redundant switches still loses everything when one DNS resolver goes down. A synthetic twin of a made-up branch network shows the hidden dependency and what removing it takes."
tags: ["DNS", "branch office", "single point of failure", "network design", "routing", "synthetic twin", "RKR SETU"]
slug: "branch-dns-resolver-single-point-of-failure"
audio: ["/audio/branch-dns-resolver-single-point-of-failure.mp3"]
audioDuration: "4:18"
cover:
  image: "/covers/branch-dns-resolver-single-point-of-failure.jpg"
  alt: "When one DNS resolver goes, the branch goes: finding hidden dependencies (cover image)"
  hiddenInSingle: false
seoTitle: "Branch DNS resolver: the single point of failure to find first"
seoDescription: "A branch with two internet links and redundant switches still goes dark when one DNS resolver fails. Find the hidden dependency in a synthetic twin first."
categories: ["Outages and failover"]
---

The branch had two internet links, two firewalls in a pair, two core switches and a backup LTE router in the cupboard. It was, by every design review, a resilient site. Then the small server in the comms room that ran DNS for the branch went down for a firmware update, and for forty minutes nobody could open anything.

Every link was up. Every route was in place. Names just would not resolve.

## Resilient paths, one resolver

DNS is easy to overlook because it is so reliable. A branch client asks for a name, the resolver answers, and the client connects. When the resolver is unreachable, every application that starts with a name fails, which is almost all of them.

In many branches, the resolver is a local box or a service on the firewall, set up once and handed out through DHCP. Sometimes a second resolver is configured too, but it points back across the WAN to the head office, through the same firewall pair, or to an address that only works when the primary tunnel is up. On paper there are two. In practice they share a fate.

There is also the question of what clients do when the first resolver fails. Some move to the second quickly. Some wait for a long timeout on every lookup. Some cache the failure. A second resolver that the clients rarely try is not much better than none.

## Why redundancy reviews miss it

Network reviews look at links, devices and routes. Server reviews look at the hosts in the data center. A small DNS service in a branch comms room falls between the two. It is not network equipment, and it is not a data center server. Nobody owns its redundancy.

And because DNS failures look like everything failing at once, troubleshooting tends to start in the wrong place: links, firewalls, the ISP.

## Pulling the resolver in a made-up branch

Consider an illustrative branch with 120 users, two internet links, a firewall pair and a site-to-site tunnel to the head office. The synthetic twin holds the network, the DHCP settings that hand out resolvers, and the services clients depend on.

Taking the local resolver down in the twin shows the result plainly. The second resolver handed out by DHCP is at the head office, reachable only through the tunnel, and in this design the tunnel's own endpoint is configured by name. Clients that try the second resolver get answers only while the tunnel stays up. The first time the tunnel drops, it cannot look up its own endpoint to come back, the second resolver goes with it, and every user loses name resolution, even though both internet links are up.

Then try the alternatives. Configure the tunnel endpoints by address, so the tunnel does not depend on DNS. Add a resolver on the firewall pair as the second choice, which already has redundancy. Run the same failure again, and users carry on with only a short delay on the first lookup.

## A short DNS resilience check for branches

- List every resolver each branch hands out, and trace the path to each one.
- Check whether the second resolver depends on the same device, tunnel or link as the first.
- Make sure tunnels, management access and monitoring do not rely on DNS to come back up.
- Test how your common client types behave when the first resolver stops answering.
- Give the branch DNS service a clear owner and include it in maintenance plans.
- When a whole site fails with links up, check name resolution early.

Branch resilience is usually built one layer at a time. DNS sits across all of them, which is why it is so often the one layer nobody doubled.

Related reading: [proving you are really redundant]({{< ref "rkr-podcast-ep03-fully-redundant-prove-it.md" >}}), [what goes dark when the UPS is on battery]({{< ref "ups-on-battery-what-goes-dark.md" >}}) and [a dual-homed server on the wrong path]({{< ref "dual-homed-server-wrong-path-after-reboot.md" >}}). More in the [outages and failover guide](/outages-and-failover/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
