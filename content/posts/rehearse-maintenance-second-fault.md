---
title: "Busway maintenance tonight: rehearse it, and the second fault, before the window"
date: 2026-10-31
description: "Planned maintenance uses up one side of your power redundancy. Rehearse it on a synthetic twin to see what one more tripped breaker would do to a 1,024-GPU training job."
tags: ["maintenance window", "change management", "N-2", "power resilience", "data center", "synthetic twin"]
slug: "rehearse-maintenance-second-fault"
audio: ["/audio/rehearse-maintenance-second-fault.mp3"]
cover:
  image: "/covers/rehearse-maintenance-second-fault.jpg"
  alt: "Busway maintenance tonight: rehearse it, and the second fault, before the window (cover image)"
  hiddenInSingle: false
---

Tonight there's maintenance on one busway in the hall. The work is planned, the method statement is signed off, and the check says nothing loses power. One training job is running across every GPU in the room. The question everyone asks is simple: is it safe? The question that usually goes unasked is harder: safe until what?

## How this usually goes

Most maintenance checks answer one question. If we take this side of the power out, does anything go down? In a hall built with A and B feeds the honest answer is usually no. Every rack has a second path, so the work goes ahead.

What that check doesn't show is what the maintenance uses up. While one busway is isolated, every rack it fed is running on its other side alone. Nothing has failed, but the redundancy that was there this morning is gone for the length of the window. One more fault, a tripped breaker, a loose connection, a power supply giving up, now lands on a hall that has no spare.

That second fault is the one that turns a routine night into an incident. And because it's unplanned, it rarely gets rehearsed. The plan covers the work. It doesn't cover what happens if something else goes wrong during the work.

In an AI hall the cost of getting this wrong is unusually clear. A large training job is spread across hundreds or thousands of GPUs, and it typically needs all of them. Losing a handful of servers doesn't slow the job down. It stops it.

## The two questions that matter

Before the window opens, the team needs two answers.

First, is the planned work itself safe? What loses power, what drops to a single feed, and how close does the remaining side get to its rating?

Second, what is one breaker away from stopping the job while the work is in progress? Not "row C is at reduced redundancy", but which devices lose power if one more breaker trips, which servers go down, and whether the job survives it.

## The same night on a synthetic twin

The demo below works this scenario on a synthetic twin of a made-up AI hall, from one CLI session. All figures come from declared design data: an engineered layout and its power sizing, a declared server power supply split, design loads and training-job parameters. The maintenance and the fault were applied in this take, and the figures were computed in this take. Nothing here is measured from a live site.

<!-- Video: setu_1_0_n. Replace d0JTZKQi3IM with the YouTube ID once it is uploaded. -->
{{< youtube d0JTZKQi3IM >}}

The hall has four rows of 256 GPUs, 1,024 in total, and the training job needs every one of them.

Tonight's work is on busway C-A. SETU previews it first, without changing anything. No device loses power, 59 devices drop to a reduced supply, and the job keeps running. That's the answer most checks stop at.

The busway is then isolated. The other side, busway C-B, now carries row C alone at 57 percent of its rating. Nothing is near its limit and the job is fine. But row C now runs on one side.

So the next question is asked before anything else happens. If one tap-off breaker in row C trips now, what goes down? The preview is specific: 5 devices lose power, 4 servers go down, 32 GPUs drop out, and the whole job stops.

In the demo, at 02:40, that breaker trips. The rack turns red and the job stops. Three of the rack's four power feeds have no supply.

The alarms tell the story in one line. There are three of them, and they share one root cause: busway C-A and that breaker, together. On its own, the breaker would have taken nothing down. Neither would the maintenance. Together, they stop the job.

The cost is stated on the declared job parameters rather than measured: up to 938.7 GPU-hours of lost work, counting the time since the last checkpoint, the time to detect and the time to restart, plus 1,024 GPU-hours sitting idle for every hour it stays down.

Power is restored and the job runs again from its last checkpoint. A 1-page power report records what lost power, the 32 GPUs out, and how it came back.

To sum up the take: 59 devices on one feed during the maintenance and none lost, 5 devices shown losing power before the breaker tripped, and 32 GPUs out when it did.

## Why the second fault deserves a rehearsal

Planned work is rehearsed because it's planned. The second fault isn't, so it tends to live as a vague risk in the change request: "reduced redundancy during works". That phrase is true, and it doesn't help anyone decide anything.

Seeing the second fault before the window changes the conversation. If the team knows that one breaker in row C is all that stands between the maintenance and a stopped job, there are real options. Move the job to a checkpoint just before the window. Check that breaker and its load before isolating the busway. Shorten the window, split the work, or choose a night when the job can tolerate a stop.

None of that needs a new tool in the moment. It needs the answer to have been on screen before the work started. In the demo, the second fault was on screen before it ever happened.

The same thinking applies well beyond GPU halls. Any time planned work uses up one side of a redundant design, the useful question is what one more failure would do while it's out. If you've read how we [rehearse a switch replacement before the maintenance window]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}), this is the same habit applied to power.

## Practical takeaways

- Treat planned maintenance as a temporary loss of redundancy, not just a list of steps. Write down what runs on one side while the work is in progress.
- Before the window, ask what one more fault would do, not only whether the planned work is safe. Pick the most likely second fault and look at its impact.
- State the impact in terms the business understands: which servers, how many GPUs, and whether the job stops or carries on.
- Check headroom on the side that stays live. A busway at 57 percent of its rating is fine, but know the number before you rely on it.
- Plan the job around the window. A fresh checkpoint just before the work starts limits what a stop can cost.
- After the window, keep the report. What lost power and how it came back is the starting point for the next plan.

For the bigger picture, start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}). For another power story, see [what goes dark when the UPS is on battery]({{< ref "ups-on-battery-what-goes-dark.md" >}}).

Rehearse the maintenance, and the second fault, before tonight. We build synthetic twins for all.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
