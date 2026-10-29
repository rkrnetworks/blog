---
title: "RKR Podcast, episode 3: we're fully redundant. Prove it."
date: 2026-10-29T10:10:00Z
description: "A network lead brings the line every team says in the first meeting: we're fully redundant. An RKR technical marketing engineer answers with recorded SETU 1.0 demos. The idea running through the episode: redundancy is a claim until you've tested it."
tags: ["podcast", "redundancy", "single point of failure", "N-2", "maintenance window", "synthetic twin"]
slug: "rkr-podcast-ep03-fully-redundant-prove-it"
audio: ["/audio/rkr-podcast-ep03-fully-redundant-prove-it.mp3"]
audioDuration: "4:54"
cover:
  image: "/covers/rkr-podcast-ep03-fully-redundant-prove-it.jpg"
  alt: "RKR Podcast, episode 3: we're fully redundant. Prove it. (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 3. YouTube ID Y-bFm8qzwgw. Routing note matches the pinned YouTube comment (/workspace/youtube/ep03/note.txt).
seoTitle: "Fully redundant? How to prove it | RKR Podcast 3"
seoDescription: "Every team says it is fully redundant in the first meeting. An RKR engineer answers with recorded SETU 1.0 demos: redundancy is a claim until it is tested."
categories: ["Podcast", "Outages and failover"]
---

> Update, Oct 27, 2026: since this was recorded, a new demo shows a routing change on a synthetic twin, with routes withdrawn and failover checked against a baseline: https://youtu.be/ezmcUdKr4bo

Every team says it in the first meeting: we're fully redundant. Two of everything. The design review says no single point of failure.

That's episode 3 of the RKR Networks Podcast. A network lead is back in the customer's chair. An RKR technical marketing engineer answers with recorded SETU 1.0 demos.

Everything discussed comes from recorded SETU demos run on made-up example sites. Both voices are AI-generated.

## Watch or listen

{{< youtube Y-bFm8qzwgw >}}

Prefer audio? The episode is also on the [RKR Podcast on Spotify](https://open.spotify.com/show/4uqMIzZcJCOMJ1utAEjNIJ). Every question, with its timestamp, is in the YouTube description.

## A riser six floors share

The building has two rising mains. Six closets go on battery at once, and one question traces every alarm to one failed rising main.

The preview, with nothing changed, shows 6 switches down, 43 access points off air and 95 devices offline. 13 can roam.

The one-page report lists what lost power and the single points of failure that remain. That building had 24 of them. The six switches that lost power each had one power input, and needed it.

That list is a fix plan. Some fixes are quick, like a second feed. Others go to the next budget.

## One switch, then two

On a made-up office floor, one switch fails. All 22 affected Wi-Fi clients roam. None are stranded.

Two fail together. 6 clients go dark, and one subnet loses its gateway with no standby. Nothing was set up to take over. That kind of double failure is hard to reason about on paper.

Wi-Fi overlap has the same catch. Overlapping access points on one switch, one closet or one feed fail together. A coverage map won't show that.

## The second fault during maintenance

With A and B feeds, most maintenance checks ask one question: does anything go down? The usual answer is no.

On a made-up AI hall with 1,024 GPUs, the busway preview says no device loses power. 59 drop to a reduced supply, and the job keeps running. That's where most checks stop.

The next question is the one that matters. If one tap-off breaker trips now, 5 devices lose power, 4 servers go down, 32 GPUs drop out and the whole job stops.

Neither fault alone takes anything down. Together, they stop the job. "Reduced redundancy during works" is true, and it doesn't help anyone decide.

## A setting, not a box

A VLAN pruned from one end of a trunk applies cleanly, with no error and no warning. Every link stays up. Login still breaks, because the authentication path was on that VLAN.

A single point of failure can be a setting, not only a box. In another demo, every port on a two-host cluster stayed up, and new clients still got no IP address. The links never went down. A decision did.

It can also be a path. In a made-up retail estate, losing one shared WAN path cut 10 sites off at once.

Verify services, not only links: authentication, DHCP and name resolution.

## Practical takeaways

- Treat redundancy as a claim until you've tested it.
- Test one failure, then two. Start with pairs that share a feed, a closet or a path.
- N plus one means one spare for one failure, and only if the spare doesn't share a feed, a closet or a path.
- Before a window, write down what runs on one side, and pick the most likely second fault.
- Keep a running list of single points of failure. Every scenario adds to it or crosses something off.

For the written versions, read [what goes dark when the UPS is on battery]({{< ref "ups-on-battery-what-goes-dark.md" >}}), [the maintenance and the second fault]({{< ref "rehearse-maintenance-second-fault.md" >}}) and [one pruned VLAN breaks authentication]({{< ref "pruned-vlan-breaks-authentication-every-link-up.md" >}}). The routing change from the update above is in [one deny line, 289 flows blocked]({{< ref "one-deny-line-289-flows-rehearse-the-change.md" >}}).

Rehearse every change on the synthetic twin before it goes live.

Related reading: [a branch DNS resolver as a single point of failure]({{< ref "branch-dns-resolver-single-point-of-failure.md" >}}). More in the [RKR Podcast page](/podcast/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
