---
title: "UPS on battery: how to know what goes dark before it does"
date: 2026-10-27
description: "Six closets report UPS on battery. Here's how to find the one root cause and predict which switches, APs and devices go dark before the batteries run out."
tags: ["UPS", "power resilience", "root cause analysis", "alarm correlation", "single point of failure", "synthetic twin"]
slug: "ups-on-battery-what-goes-dark"
cover:
  image: "/covers/ups-on-battery-what-goes-dark.jpg"
  alt: "UPS on battery: how to know what goes dark before it does (cover image)"
  hiddenInSingle: false
---

An alarm comes in: six comms closets say their UPS is on battery. Nothing is down yet. The question everyone asks next is simple, and in most buildings nobody can answer it quickly. When the batteries run out, what goes dark?

## How this usually goes

A power event is one of the worst kinds of alarm flood. Each UPS raises its own alarm. Then the switches behind them start complaining, then the access points, then the monitoring system notices clients dropping. Within a few minutes there are dozens of separate alerts, and they all look urgent.

At the same time the problem sits across two teams. Facilities looks at the power side: utility, generator, distribution, UPSs. The network team looks at switches and APs. They're often working from different screens, and neither has the whole picture.

So the usual response is a mix of guesswork and phone calls. Someone checks the UPS runtimes. Someone else tries to remember which closet feeds which floor. People argue about whether it's one problem or six. And very often the real impact only becomes clear when the batteries run out and things actually go dark.

Closet UPS runtime is usually measured in minutes, not hours. Every minute spent working out what is going on is a minute not spent acting on it.

## The two questions that matter

When closets go to battery, the network team needs two answers fast.

First, is this one problem or many? If six UPSs went to battery at the same moment, the odds are they share something upstream. Finding that shared cause turns a flood of alarms into a single incident with one place to send people.

Second, what is the network impact if the batteries run out? Not "floor 9 might be affected", but which switches, how many access points, how many devices, and whether anyone can roam to a neighbouring AP that stays up.

## The same alarm on a synthetic twin

The demo below works this exact scenario on a synthetic twin of a made-up example building, from one CLI session. The fault was introduced before the take, and the 15-minute battery runtime is part of the building's declared supply plan.

{{< youtube 5lP9lirH2Q0 >}}

It starts with the supply side of the building: utility, generator, two rising mains, and a UPS in each floor closet. The UPSs on six upper floors are on battery. Nothing is down yet, and the plan gives 15 minutes.

Next comes the root cause. One question traces every alarm back to a single failed rising main. That takes about 15 seconds from the alarm. Following any one switch's supply on those floors leads back to the same failed riser, so the network and the power behind it are finally in the same picture.

Then comes the question that matters. With 15 minutes of battery, what goes dark when it runs out? SETU previews it without changing anything: 6 switches down, 43 APs off-air and 95 devices offline, with 13 devices able to roam to a neighbouring AP.

That's the moment the 15 minutes becomes useful. You can send someone to the right closet, warn the people on the affected floors, and decide what to protect first.

In the demo, nobody gets on site in time. The batteries run out and the upper floors go dark. The measured impact matches the prediction: 43 of 85 APs off-air and 95 of 280 devices offline, with the coverage holes shown floor by floor. Asking for the cause again still points at the same rising main.

Finally, power is restored and everything comes back. A 1-page PDF report captures the timeline, the root cause, the devices that lost power, and the single points of failure that remain. In this building, 24 are listed.

To sum up the take: 15 seconds from the alarm to the one fault behind it, 6 closets on battery traced to one rising main, 95 guest devices predicted offline before the batteries ran out and 95 measured offline when they did, and 43 APs on six floors known 15 minutes early.

## Why the prediction matters more than the alarm

Most tools are good at telling you something has happened. A UPS on battery is a fact. What a team actually needs in that moment is the consequence, stated in network terms: these switches, these APs, these floors, this many people.

Having the prediction early changes the response. Instead of everyone looking at alarms, one person goes to the closet that matters and someone else sends a note to the affected floors. The team decides calmly what needs protecting first.

The report afterwards is just as useful. Twenty-four single points of failure is a fix plan, not just an incident record. Some of those will be cheap to fix, like a second feed or moving a critical device to a closet on the other riser. Others go into the next budget. Either way, they're written down before the next power event finds them.

SETU works alongside the Cisco, Aruba, Juniper and Arista gear you already run, and RKR doesn't sell hardware.

Outages don't wait, and neither do attackers. Both tend to find the single points of failure you haven't listed yet. Attackers practice. Your engineers should too.

## Practical takeaways

- When several UPSs go to battery at once, assume a shared upstream cause until proven otherwise. Look for the common feed before working each alarm on its own.
- Keep the power path and the network in one picture. Knowing which rising main, panel or UPS feeds each closet turns a guess into a short list.
- Know your declared runtime per closet. Fifteen minutes is enough time to act if you know where to look, and not much time if you don't.
- Decide in advance what you would protect first if power runs short, so the call isn't made during the incident.
- After every power event, write down the single points of failure it exposed, and track them like any other fix.

If you're curious how the same idea handles a quieter problem, the next post follows [a Wi-Fi ticket down to one cable]({{< ref "wifi-keeps-dropping-trace-ticket-to-one-cable.md" >}}). For the bigger picture, start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
