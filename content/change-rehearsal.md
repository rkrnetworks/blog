---
title: "Change rehearsal: test every network change before the window"
seoTitle: "Network change rehearsal: find the blast radius before the window"
description: "Why reviewed changes still cause outages, what rehearsing a change actually means, and every post that walks a real change through a synthetic twin first."
seoDescription: "Reviewed network changes still break things at 2 AM. Learn how to rehearse a change, measure its blast radius and bring evidence to the change board."
url: "/change-rehearsal/"
layout: "hub"
hubCategory: "Change rehearsal"
breadcrumb: "Change rehearsal"
date: 2026-10-29
hiddenInRss: true
cover:
  image: "/images/hubs/change-rehearsal.jpg"
  alt: "Network change rehearsal guide from RKR Networks"
---

Most outages are not caused by hardware failing on its own. They follow a change: a firewall rule, a route withdrawal, a trunk tidy-up, a switch swap, a certificate renewal. The change was reviewed, approved and scheduled in a maintenance window, and it still surprised someone. This guide explains why, and what it means to rehearse a change rather than just review it.

## Why reviewed changes still break things

A change request lists the lines that will change. It rarely lists the **traffic** that will change. Reviewers read the diff, not the consequences. A few patterns account for a large share of surprises:

- **Order matters.** Access lists and route policies are read top to bottom. A line in the wrong place can win over every line below it, and nothing in the diff looks wrong. See [one deny line that blocked 289 flows]({{< ref "posts/one-deny-line-289-flows-rehearse-the-change.md" >}}).
- **Hidden dependencies.** A rule with no hits for a year may be waiting for a quarterly job. A certificate may be pinned by one application nobody remembers. See [firewall rule cleanup]({{< ref "posts/firewall-rule-cleanup-unused-rule-still-needed.md" >}}) and [a certificate rotation that broke one app]({{< ref "posts/certificate-rotation-breaks-tls-inspection.md" >}}).
- **Everything stays green.** A pruned VLAN can leave every link and every peer up while nobody can log in. Monitoring checks that things are up, not that they work together. See [one pruned VLAN]({{< ref "posts/pruned-vlan-breaks-authentication-every-link-up.md" >}}).
- **Side effects of new hardware.** A new access switch with default settings can become **spanning tree root** and pull a floor's traffic the long way round. See [when a new switch became root]({{< ref "posts/new-switch-becomes-spanning-tree-root.md" >}}).
- **Routing reaches further than expected.** A maintenance change on one edge router can leak routes well beyond the site. See [a BGP route leak after maintenance]({{< ref "posts/bgp-route-leak-after-maintenance-blast-radius.md" >}}).

## Review, test and rehearse are different things

**Peer review** catches mistakes in the plan. **Lab testing** proves a feature or a firmware version works on a few spare devices. **Rollback plans** limit how long the damage lasts. All are worth doing, and none tells you, in advance, what this change will do to this site.

**Rehearsal** means applying the planned change to a model of the real site and looking at the result: which flows changed, which hosts lost a path, which access points and users were affected, and what happens if something else fails during the window. That result is the **blast radius** of the change.

## A rehearsal workflow

1. **Freeze a starting point.** Take the site as it is now, in the model.
2. **Apply the change as written.** Not a summary of it, the actual lines.
3. **Diff the behaviour, not the config.** Count the flows, routes and reachability that changed, and list who owns them.
4. **Add a second fault.** Maintenance uses up one side of your redundancy. What would one more failure do? See [rehearsing maintenance and the second fault]({{< ref "posts/rehearse-maintenance-second-fault.md" >}}).
5. **Fix and re-check from the same start.** A clean re-check is zero unexpected changes.
6. **Bring a one-page report to the change board.** What changes, for whom, and how you checked it. The conversation gets shorter.

## What to rehearse first

You cannot rehearse everything on day one. Start with changes that are frequent, risky or both:

- Access list and firewall policy changes
- Route withdrawals, redistribution and BGP policy
- Trunk and VLAN clean-ups
- Switch and access point replacements. See [rehearsing a switch swap at 2 AM]({{< ref "posts/rehearse-switch-replacement-before-maintenance-window.md" >}})
- QoS policy changes, where the effect shows up as late packets rather than lost ones. See [packets that arrive but still miss the deadline]({{< ref "posts/qos-packet-arrives-still-late.md" >}})
- Power and facilities maintenance in the data hall

Keep a running list of single points of failure. Every rehearsal should add to it or cross something off.

## Why a synthetic twin

Rehearsal needs a model you can break without consequences, built from your own site rather than a lab topology. A synthetic twin of the network and building gives you exactly that: apply the change, see the blast radius, rewind, try again. The posts below each take one change from plan to clean re-check on a made-up site.

The [first episode of the RKR Podcast](/podcast/) is a conversation about this idea: rehearse every change before it goes live. Terms like ACL, VRF and N-2 are explained in the [glossary](/glossary/).
