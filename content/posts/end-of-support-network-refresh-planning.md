---
title: "End-of-support network equipment: plan the refresh by impact, not age"
date: 2026-10-30
description: "Half your gear may be past its maker's support. Fail the oldest core on a synthetic twin to see what it carries, and rank the refresh by impact, not age."
tags: ["end of life", "network refresh planning", "lifecycle management", "core switch", "single point of failure", "synthetic twin"]
slug: "end-of-support-network-refresh-planning"
cover:
  image: "/covers/end-of-support-network-refresh-planning.jpg"
  alt: "End-of-support network equipment: plan the refresh by impact, not age (cover image)"
  hiddenInSingle: false
audio: ["/audio/end-of-support-network-refresh-planning.mp3"]
audioDuration: "6:38"
---

Most networks are a mix. New Wi-Fi 6E access points sit next to Wi-Fi 4 units that have been on the ceiling for a decade. The access layer is current, and the core is a switch nobody wants to touch. Some of that gear stopped getting support from its maker years ago, and everyone knows it. The hard question isn't whether to refresh, but what to replace first with the budget you have.

## How refresh planning usually goes

The usual method is familiar to anyone who has done it. Build a spreadsheet of models and serial numbers. Check each maker's end-of-life notices one by one and note the end-of-sale and end-of-support dates. Then make a judgement about what each old box would take down if it failed.

That last step is where it gets shaky. It's mostly guesswork, done from diagrams and memory. So refresh plans tend to fall back on the one thing that is easy to measure, which is age. The oldest gear goes first, and the real risk shows up during an outage.

Most refresh guides already say the right thing: prioritise by risk and blast radius, not by age, and start with the devices everything else depends on. The problem is showing it. "This core switch is high risk" is a hard sell to a budget holder without something concrete behind it.

## The same refresh on a synthetic twin

The demo below works through it on a synthetic twin of a made-up example building, from one CLI session. End-of-support dates follow each maker's published notices, and makers are not named.

{{< youtube S7HkRH0vdlU >}}

It starts with one command that lists every device generation in the building, with its end-of-sale and end-of-support dates. The Wi-Fi 4 APs lost support 4 years ago and Wi-Fi 5 Wave 1 3 years ago. One Wave 2 model ends this month and another in 12 months, while the newest access switches and Wi-Fi 6E APs are current. Old or new, every device is modelled and tested the same way, supported or not.

Across the building, 44 devices are past their maker's support, including the core, which has been out of support since 2019.

Looking at that core shows a 64-port 10G aggregation switch released in 2011, with support that ended 7 years ago. Two more switches show the same trunk port written in different command styles. That's three command styles in one building, all in one model of the network, which is what mixed estates look like in real life.

Then comes the real question: what happens if that 2011 core fails? SETU rehearses it on the twin without touching anything real. Coverage holes open up across the floors and the building turns red. The routing impact shows too. Several networks lose their gateway with no standby, so hosts can't reach anything off their own subnet. A simple map of cables and ports would miss that part. In this example, 212 guest devices would be stranded.

Finally there's a 2-page PDF report covering 98 devices, 44 past maker support and 36 more ending within 12 months. Replace first: R90-SW01, the 2011 core, because it carries the whole tower.

To summarise the example building: 44 of 98 devices past their maker's support, modelled like the new ones; the oldest support end in the building was 2018-06; three command styles in one model; and 212 guest devices stranded if the old core fails, known before it does.

## Ranking by impact changes the conversation

The useful part isn't the list of dates. Most teams can build that list with enough patience. What matters is being able to say, for each old box, what happens when it fails.

Once you can, the order often changes. An old access switch on a quiet floor might be older than anything else on the list and still not matter much. A core switch carrying the whole tower, with networks that have no standby gateway behind it, goes to the top even if something else has an older date. That's spending the budget on the box that carries the most, not the one with the oldest date.

It also gives management something they can read. A 2-page report that says "replace this first, because if it fails 212 devices are stranded and several networks lose their gateway" is a different conversation from "this switch is old."

There's a security side too. Unsupported gear stops getting security fixes, and attackers look for exactly that. Knowing which unsupported boxes matter most tells you where to put compensating controls while the refresh is waiting for budget. Attackers practice. Your engineers should too.

SETU works across mixed gear and different command styles, alongside the Cisco, Aruba, Juniper and Arista equipment you already run. RKR doesn't sell hardware, so the replace-first list is about your plan, not our catalogue.

## Practical takeaways

- Track end-of-support, not just end-of-sale. End-of-support is when security fixes stop, and that's the date that matters for risk.
- Put old and new gear in the same view. A refresh plan built only from the old gear misses what the new gear depends on.
- For each out-of-support device, answer one question: what goes dark if this fails tonight? Rank the refresh by that answer.
- Look past the cabling. Lost gateways with no standby are easy to miss on a port map and often the bigger part of the impact.
- Watch the next 12 months as closely as the past. In the example, 36 more devices reach end of support within 12 months, on top of the 44 already past it.
- Bring a short report to the budget meeting, with a replace-first line and the reason in plain words.

To see how the same "what if it fails" approach works for a planned change, read [rehearsing a 2 AM switch swap]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}). For the basics, start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
