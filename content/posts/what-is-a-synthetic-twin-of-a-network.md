---
title: "What is a synthetic twin of a network?"
date: 2026-10-26
description: "A synthetic twin is a model of your network you can question, break and rewind, so you can see what a change or failure does before production does."
tags: ["synthetic twin", "change management", "blast radius", "network engineering", "single point of failure"]
slug: "what-is-a-synthetic-twin-of-a-network"
cover:
  image: "/covers/what-is-a-synthetic-twin-of-a-network.jpg"
  alt: "What is a synthetic twin of a network? (cover image)"
  hiddenInSingle: false
audio: ["/audio/what-is-a-synthetic-twin-of-a-network.mp3"]
audioDuration: "6:46"
---

Every network engineer has a version of the same question. If I change this, what breaks? If this box dies tonight, who calls? Usually the honest answer is "probably nothing, but we'll find out." This post explains what a synthetic twin is and what it looks like in practice.

## The problem: production is the only test bench most teams have

Most networks are documented in a mix of places: a cabling spreadsheet, diagrams of different ages, the controller's view of the APs, and whatever the senior engineer remembers. To work out what a change or failure would do, someone pulls those together in their head.

Then the change goes in during a maintenance window and the network gives the real answer. If something was missed, it turns up on a bridge call at 2 AM, or as tickets the next morning.

Teams know this, so they work around it. A lab with a few spare switches is good for testing a feature or a firmware version, but it rarely looks like the real building, with its floors, closets, cable runs and client counts. Peer review catches mistakes in the plan, but not things nobody wrote down. Change windows and rollback plans limit the damage without telling you in advance what the damage will be. Monitoring tells you what broke after it broke.

None of these let you ask "what if?" about your actual site and get a specific answer before you touch anything.

## What a synthetic twin is

A synthetic twin is a working model of a network and the building it lives in: floors, closets, switches, access points, cables, the Wi-Fi clients on them, and the power behind them. It isn't a picture. You can ask it questions, change it, fail parts of it and watch what happens, then put it back.

The word "synthetic" matters. The twin is where you break things on purpose. Nothing you do there reaches production, so you can fail two switches at once, cut a cable, or run the batteries flat.

In practice, that means a team can ask where things are and how they connect, preview the impact of a change or failure without applying it, actually fail something in the model and rewind, and export the result as a report a change board or manager can read.

## What it looks like: one session on an office floor

The video below is one unedited session on SETU's CLI, typed in a single take. The site is a made-up office floor with 3 switches, 16 access points and 56 cables.

{{< youtube 3PWsWo84VH4 >}}

Here's what happens in under three minutes:

- Where does a VLAN actually run? Ask for one VLAN and every cable that carries it lights up. Normally that answer lives in a spreadsheet that may or may not be current.
- What path does traffic take? A test frame between two devices is delivered, routed across two routers. Then the real path between two hosts is shown hop by hop and cable by cable, across three physical routes.
- What if one switch fails? All 22 affected Wi-Fi clients roam to neighbouring access points. None are stranded.
- What if two fail together? This is where it gets interesting. Six clients go dark, some Wi-Fi cells lose their backup, and one subnet loses its gateway with no standby. That kind of double failure is hard to reason about on paper.
- Write it down. The full impact goes into a short report before anyone touches a thing.
- Break it, then rewind. A point in time is marked and a switch is failed in the model. Its power is pulled, the damage shows across the floor, and a ping to a host behind it gets nothing back. Then the model rewinds to the mark, hosts get their gateway back, the access points recover, and the ping answers.

In this take the full blast of losing a switch, across cabling, switching, routing and Wi-Fi, was worked out in 13 ms. Testing the change end to end (fail it, check it, undo it) took 31 seconds, and no production devices were touched.

## Where it helps day to day

Over the next few posts we'll go through four everyday jobs, each with its own demo:

- Root cause. One fault often shows up as a flood of alarms. A twin can trace them back to the one thing that failed. In [our UPS demo]({{< ref "ups-on-battery-what-goes-dark.md" >}}), six closets on battery trace back to one failed rising main.
- Ticket triage. A Wi-Fi ticket can be followed from the floor down to [one cable in a closet]({{< ref "wifi-keeps-dropping-trace-ticket-to-one-cable.md" >}}), without logging into a single device.
- Change rehearsal. A switch swap can be [rehearsed before the maintenance window]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}), so you know which hosts, APs and users get hit, and can plan for them.
- Refresh planning. Out-of-support gear can be [failed in the model to rank the refresh]({{< ref "end-of-support-network-refresh-planning.md" >}}) by what each box carries, not by its age.

## What a synthetic twin is not

It doesn't replace your monitoring. Monitoring tells you what is happening. A twin answers what would happen if.

It doesn't replace your gear or your vendors. SETU works alongside the Cisco, Aruba, Juniper and Arista equipment you already run. RKR doesn't sell hardware.

And it doesn't replace engineering judgement. It gives the engineer a specific answer to start from instead of a guess.

## Why we care about it

Outages and attackers both find the weak spots you haven't looked at, like the subnet with no standby gateway or the switch everything quietly depends on. A twin is a safe place to find them first. Attackers practice. Your engineers should too.

## Practical takeaways

- Write down the "what if" questions your team actually gets asked: a switch swap, a closet losing power, a core failing, a floor with bad Wi-Fi. Those are the scenarios worth rehearsing.
- Test double failures, not just single ones. In the demo, one switch failing stranded nobody. Two failing together stranded six clients and left a subnet without a gateway.
- Treat the impact report as part of the change, not an extra. If the change board can see the blast radius, the conversation gets shorter.
- Keep a running list of single points of failure. Every scenario you run should add to it or cross something off.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
