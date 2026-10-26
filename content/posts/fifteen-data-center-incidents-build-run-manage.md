---
title: "Build it, run it, manage it: 15 data center incidents in one synthetic twin"
date: 2026-10-26T07:15:00Z
description: "A data hall built from nothing, switched on, and then things break: stale sensors, flapping ports, a fibre trunk cut, a leak under the floor and more. Fifteen incidents, each placed in one synthetic twin."
tags: ["data center", "DC operations", "incident management", "power and cooling", "root cause analysis", "synthetic twin", "RKR SETU"]
slug: "fifteen-data-center-incidents-build-run-manage"
audio: ["/audio/fifteen-data-center-incidents-build-run-manage.mp3"]
audioDuration: "3:51"
cover:
  image: "/covers/fifteen-data-center-incidents-build-run-manage.jpg"
  alt: "Build it, run it, manage it: 15 data center incidents in one synthetic twin (cover image)"
  hiddenInSingle: false
---

Last time we built it. This time we switch it on, and things break the way they do on any live floor.

A data hall doesn't fail in one way. On a normal week, the ops team, the technicians and the electricians might see a sensor that stops reporting, a port that won't settle, a door left open, and a breaker that trips for no obvious reason. Each one lands with a different person, in a different tool. This post is about seeing all of them in one place.

## How incidents usually arrive

In most halls, the network, the power and the cooling are watched separately. A link error shows up for the network team. A warm busway joint is an electrical issue. A leak under the floor belongs to facilities. Each team sees its own part clearly, and nobody sees how they fit together.

So the first questions in an incident are often the same. Where is it, what is it connected to, and who else should know? Answering them can take longer than fixing the fault.

## A live hall in a synthetic twin

The video below builds a made-up data center from nothing in a synthetic twin, and then runs it live.

{{< youtube sM5zjELKGuI >}}

Watch it on YouTube: https://youtu.be/sM5zjELKGuI

First the shell of the hall, then the steel overhead. Cable trays and lighting follow, laid out across the ceiling. Down the aisles, the layout takes shape. The pedestals go down and the raised floor goes over them. Then the racks and cabinets, row by row, with the overhead units above. Outside, the container and the plant that keep the hall running.

Now the hall is live, with cool air moving through the aisles. And then things start to go wrong.

A stale sensor. A port flapping. A cracked floor tile. Spine link errors, low light on an optic, and a containment door left open. A busway joint running warm. A switch power supply fails, and the console path is lost. A PDU outlet goes down. Then a fibre trunk is cut. A tap-off breaker trips. A leaf switch drops. Water under the floor. And a pump in the cooling distribution unit faults.

That's fifteen incidents. One by one, each fault is found and worked through, and each one is placed in the synthetic twin.

How many of them have you experienced?

## Why one model for every kind of fault

Look at that list again. Some of it is network, some is power, some is cooling, and some is just the building. A cracked tile and a cut fibre trunk have nothing in common, except that they happen in the same hall and can affect the same racks.

When every fault is placed in one model, the questions change. Not "whose problem is this?" but "what does it touch?" The aim is for every issue to be identified and understood in seconds, with the whole team on the same page. That's what we're building with SETU 1.0.

If you saw the build-out in [one team, one page]({{< ref "data-center-build-out-one-team-one-page.md" >}}), this is the same idea carried into operations. For a closer look at one power fault, see [rehearsing maintenance and the second fault]({{< ref "rehearse-maintenance-second-fault.md" >}}).

## Practical takeaways

- List the last fifteen incidents in your hall and note which team each one landed with. The spread is usually wider than expected.
- Place every fault in the same model as the racks, power and cooling, so its reach is clear from the start.
- Treat stale data as an incident. A sensor that stops reporting hides the next problem.
- Keep the model you built with. The plan for the hall is the best starting point for running it.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
