---
title: "One deny line, 289 flows blocked: rehearse the change before the window"
date: 2026-10-27T10:26:00Z
description: "Two planned changes on an office campus: withdraw two routes and close the server farm. Rehearsed on a synthetic twin first, one deny line turned out to block 289 flows. Here is how it was found, fixed and checked."
tags: ["change management", "maintenance window", "access control lists", "routing", "change advisory board", "synthetic twin"]
slug: "one-deny-line-289-flows-rehearse-the-change"
audio: ["/audio/one-deny-line-289-flows-rehearse-the-change.mp3"]
audioDuration: "5:57"
cover:
  image: "/covers/one-deny-line-289-flows-rehearse-the-change.jpg"
  alt: "One deny line, 289 flows blocked: rehearse the change before the window (cover image)"
  hiddenInSingle: false
# Video: setu_1_0_o (One deny line, 289 flows blocked). YouTube ID ezmcUdKr4bo.
seoTitle: "One firewall deny line blocked 289 flows: rehearse ACL changes"
seoDescription: "A route withdrawal and an ACL change both looked small, until one deny line blocked 289 flows. Rehearse the change on a synthetic twin before the window."
categories: ["Change rehearsal"]
---

Two changes are going in tonight. One withdraws a pair of routes. The other closes off the server farm. Both look small on paper. Both have been reviewed. The question at the Change Board is always the same: what will this actually do?

## How this usually goes

A change request lists the lines that will change. It rarely lists the traffic that will change.

Routes and access rules are read top to bottom. A line in the wrong place can quietly win over every line below it. Nobody sees that in a diff. It shows up the next morning, as tickets.

The usual check is to read the config carefully and hope. A better check is to run the change against every flow on the site before anyone types it in.

## The same changes on a synthetic twin

The demo below works these two changes on a synthetic twin of a made-up office campus, from one CLI session. The flows, routes and rules are declared design data. The changes were applied in this take, and every figure was computed in this take. Nothing here is measured from a live site.

{{< youtube ezmcUdKr4bo >}}

First, the starting point is marked as "baseline". There are 10 groups and 503 flows. 456 are working. 47 are denied by policy, on purpose: guest Wi-Fi and IoT devices can't reach the app server. Nothing is unexpected.

Change 1 withdraws the edge A routes. Two static routes are removed. One prefix moves to the backup core. The other is withdrawn. The check shows the result in plain terms: 100 Staff Wi-Fi flows to the data center apps move to the backup path, and 67 flows from staff desks to the partner portal lose reach. The other 8 groups are unchanged. All 503 flows were checked in 2.46 seconds.

That is useful on its own. 67 flows losing reach is something the Change Board should know about before the window, not after.

Change 2 closes the server farm. It adds a deny at sequence 5 of the server farm access list. The check comes back with 289 flows going from allowed to denied. Staff Wi-Fi, staff desks, cameras, door panels, building controls and printers all lose access.

One line did that. The deny sits above the specific permits, so it wins first.

The impact view puts it in terms people recognise. 100 Wi-Fi users on 35 access points. 67 desks on 23 floor closets. 51 cameras, 25 door panels, 22 building controls and 24 printers. 189 wired devices in all.

## The fix, and the re-check

The fix is to move the deny from sequence 5 to sequence 900, below the permits.

The re-check is clean. 0 of 503 flows change verdict, and no routes change. Guest Wi-Fi and IoT stay denied, exactly as before. Only the deciding rule is new. The check took 2.95 seconds.

Against the baseline, two groups still differ. Both come from change 1, and both are known.

## Rewind, then report

Then the synthetic twin is restored to the "baseline" mark. It was restored and verified in 0.93 seconds. That is the synthetic twin, not a network rollback. The state hash matches the baseline, and all 10 groups match with 0 differences. Nothing was re-run.

Last, a one-page Change Board report is saved. It lists both changes, the 289 flows the broad deny would have blocked, the people and devices behind them, the fix, and the rewind.

## Why rehearse a change at all

Most outages after a change are not exotic. They are an order of lines, a route that something still depended on, a rule that was broader than intended.

Each of those is easy to find when you check every flow, and hard to find by reading. The rehearsal turns "we think it's fine" into a number: how many flows change, and whose.

It also changes the Change Board conversation. Instead of approving a diff, the board approves an outcome. 100 flows to backup. 67 lose reach. The server farm change re-checks clean.

If you've read how we [rehearse a switch replacement before the maintenance window]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}), or [the maintenance and the second fault]({{< ref "rehearse-maintenance-second-fault.md" >}}), this is the same habit applied to routes and access rules.

## Practical takeaways

- Mark a baseline before any change. Know how many flows work, and how many are denied on purpose.
- Check every change against every flow, not only the ones you expect it to touch.
- Read the result as people and devices, not only as lines. 289 flows is abstract. 100 Wi-Fi users and 51 cameras are not.
- Watch the order of rules. A broad deny above specific permits wins first.
- After a fix, re-check from the same starting point. A clean re-check is 0 flows changed.
- Bring a one-page report to the Change Board. It should say what changes, for whom, and how you checked it.

For the bigger picture, start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}).

Rehearse the change before the window. We build synthetic twins for all.

Related reading: [firewall rule cleanup]({{< ref "firewall-rule-cleanup-unused-rule-still-needed.md" >}}), [the blast radius of a BGP route leak]({{< ref "bgp-route-leak-after-maintenance-blast-radius.md" >}}) and [rehearsing every change]({{< ref "rkr-podcast-ep01-rehearse-every-change.md" >}}). More in the [change rehearsal guide](/change-rehearsal/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
