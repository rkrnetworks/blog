---
title: "Reviewed is not the same as safe: a customer's questions on one access list change (RKR Podcast ep 5)"
date: 2026-11-05T09:06:38Z
draft: false
description: "A network lead brings two small, reviewed changes. An RKR technical marketing engineer answers with a recorded SETU 1.0 demo: 503 flows, a route withdrawal that was half a failover, and one deny line at sequence 5 that blocks 289 flows."
tags: ["podcast", "access lists", "change management", "routing", "firewall rules", "synthetic twin"]
slug: "rkr-podcast-ep05-one-deny-line-289-flows"
audio: ["/audio/rkr-podcast-ep05-one-deny-line-289-flows.mp3"]
audioDuration: "5:32"
cover:
  image: "/covers/rkr-podcast-ep05-one-deny-line-289-flows.jpg"
  alt: "RKR Podcast, episode 5: one deny line, 289 flows (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 5. YouTube ID KIDqPVuHIQY.
seoTitle: "One deny line, 289 flows: questions to ask before an access list change (RKR Podcast ep 5)"
seoDescription: "A network lead questions an RKR engineer on two reviewed changes: a route withdrawal and one deny line that blocks 289 flows. Why a careful read is not enough."
categories: ["Podcast", "Routing and security"]
---

"My engineers read every line. What will a synthetic twin see that they don't?"

That's the opening question of episode 5 of the RKR Networks Podcast. A network lead is back in the customer's chair with two small, reviewed changes: withdraw a pair of routes, and close off the server farm. An RKR technical marketing engineer answers with a recorded RKR SETU 1.0 demo.

Everything discussed comes from recorded SETU demos run on made-up example sites. Both voices are synthetic text-to-speech. RKR SETU itself is pure code.

## Watch or listen

{{< youtube KIDqPVuHIQY >}}

Prefer audio? Listen to [episode 5 on Spotify](https://open.spotify.com/episode/40Gu7hnLV8lMAWi8wxd9yA). Every question, with its timestamp, is in the YouTube description.

We already wrote up the demo itself in [one deny line, 289 flows blocked]({{< ref "one-deny-line-289-flows-rehearse-the-change.md" >}}). This post covers the questions the customer asked, and the answers.

## Why isn't a careful read enough?

Reading tells you what a line says. It doesn't tell you every flow the line touches.

An access list is checked from the top down in this example, and the first line that matches wins. So the same deny line can be harmless at the bottom of a list and dangerous near the top. Most lists in the field work this way, but not every one. Check how your own platform decides.

## Start with a baseline

Before either change, the demo records a baseline: 10 groups, 503 flows. 456 work. 47 are denied on purpose by policy: Guest Wi-Fi and IoT devices trying to reach the app server.

That second number matters. If you don't know which flows are supposed to fail, you can't tell a new break from an old rule doing its job. 22 Wi-Fi clients without an address are listed as not evaluated, rather than guessed.

## Change one: "withdraw two routes"

Two static routes are removed at edge A. The check of all 503 flows took 2.46 seconds.

The result: 10.200.0.0/16 now moves to the backup core. 10.201.0.0/16 is simply gone. So the change was half a failover. 100 Staff Wi-Fi flows moved to the backup path, and 67 Staff desk flows lost reach.

Is the backup move good or bad? SETU doesn't decide that. It shows what moved, and your Change Board decides.

## Change two: one deny line at sequence 5

The second change adds a deny at sequence 5 of the SVC-FARM list on CORP-SVC. It blocks 289 flows in six groups: 100, 67, 51, 25, 22 and 24.

The customer asked the obvious question: wouldn't the author have caught it? The line looks right on its own. The problem is where it sits. Sequence 5 matches traffic before the permit lines further down ever get a look.

The board chair's view shows where the damage lands: 35 access points, 23 floor closets and 189 wired devices.

## The fix, the re-check and the rewind

The fix removes the line at sequence 5 and puts the deny at sequence 900, after the permits.

- Re-check: 0 of 503 flows changed, 0 routes changed, in 2.95 seconds.
- Against the baseline, 2 groups still differ. That's change one, which is still in place on purpose.
- Rewind took 0.93 seconds. The state hash matched, and comparing flows showed 0 differences in 2.63 seconds.

A rewind here returns the synthetic twin to a recorded state. It isn't a rollback on live gear.

## What goes to the Change Board

One page: what changed, what broke, the fix and the clean re-check. The mistake stays in the report. A board that sees the near miss trusts the clean result more.

## What the demo didn't show

The customer asked, and the answer was plain. The demo didn't show a ticketing or monitoring integration. It didn't show named-vendor configurations. Inputs come from vendor APIs or the customer's own documents.

## What your team can do on Monday

- Write down which flows should fail today, not only which should work.
- For every new deny line, ask what it matches before the lines below it.
- Check routes and rules in the same pass. A route change can hide or expose a rule problem.
- Keep the mistake in the change record.

For the related posts, read [presales with and without a synthetic twin]({{< ref "presales-with-and-without-a-synthetic-twin.md" >}}), [cleaning up a rule that still looks unused]({{< ref "firewall-rule-cleanup-unused-rule-still-needed.md" >}}) and [introducing RKR SETU 1.0]({{< ref "introducing-rkr-setu-synthetic-twin-network-it-ops.md" >}}).

Rehearse every change on the synthetic twin before it goes live.

More in the [RKR Podcast page](/podcast/).

Book a demo with our team: sales@rkr-networks.com. In person or online.
