---
title: "Firewall rule cleanup: which unused rule is still holding something up"
date: 2026-10-29T10:00:00+05:30
description: "Hit counts say a firewall rule has not matched in a year. Remove it and something breaks next quarter. A synthetic twin helps separate rules that are truly dead from rules that are waiting for a rare event."
tags: ["firewall", "rule cleanup", "network security", "change management", "blast radius", "synthetic twin", "RKR SETU"]
slug: "firewall-rule-cleanup-unused-rule-still-needed"
audio: ["/audio/firewall-rule-cleanup-unused-rule-still-needed.mp3"]
audioDuration: "4:11"
cover:
  image: "/covers/firewall-rule-cleanup-unused-rule-still-needed.jpg"
  alt: "Firewall rule cleanup: which unused rule is still holding something up (cover image)"
  hiddenInSingle: false
seoTitle: "Firewall rule cleanup: is that unused rule still needed?"
seoDescription: "Hit counts say a firewall rule has not matched in a year. Delete it and something breaks next quarter. Tell dead rules from rare-event ones in a synthetic twin."
categories: ["Change rehearsal"]
---

Every firewall that has been in service for a few years carries rules nobody can explain. A cleanup project starts with good intentions and a report of rules with zero hits. The obvious plan is to remove them.

Most of those rules really are dead. A few are not. They protect a flow that only happens at quarter end, during disaster recovery, or when a backup link takes over. Remove one of those and nothing happens for months. Then the rare event arrives, and the one path you need is blocked.

## The problem with hit counts

Hit counts tell you what happened during the period you measured. They say nothing about what would happen under conditions you did not see. A rule allowing traffic from the secondary data center to the payment gateway might show zero hits all year, because the primary data center never failed.

Hit counters also reset. A firewall reboot, an upgrade or an HA failover can wipe them, which makes a busy rule look idle. And many firewalls count only the first rule that matches, so a broad rule higher in the policy can hide a narrow rule below it that would take over if the broad one were removed.

## Why reviews do not catch it

The person reviewing the cleanup list is usually looking at the policy, not the network. To know whether a rule matters, they would need to know which paths exist between the two sides, which of those paths only appear during a failure, and which applications depend on them.

That is a network question, not a firewall question. It involves routing, failover design and application dependencies. In most organizations those sit in different teams' heads.

## Asking the twin what each rule protects

Take a made-up company with two data centers, one internet edge in each, and a pair of firewalls between the user network and the server networks. A cleanup report lists 120 rules with no hits in twelve months.

In a synthetic twin of that environment, each candidate rule can be removed in turn, and the twin asked a different question: under normal conditions, and under each failure the design is meant to survive, which flows would now be blocked?

For the large majority of the 120, the answer is none. They can go. For a handful, the answer changes when something fails. In this illustrative example, one rule only matters when the primary internet edge is down and partner traffic arrives through the secondary site. Another only matters when the backup jobs run from the disaster recovery copy. Those rules looked unused because the failures they exist for had not happened yet.

The result is a cleanup list split in two: rules that are safe to remove, and rules that protect a specific failure path, each with a short note saying which one. That second list is the part nobody could produce from hit counts alone.

## A sensible cleanup routine

- Collect hit counts over a long period, and note any reboot or failover that reset them.
- Group candidate rules by the network paths they cover, not just by source and destination addresses.
- For each candidate, ask what would be blocked under normal conditions and under each failure the design should survive.
- Check whether a broader rule above is hiding the candidate's real use.
- Disable before deleting, with a clear rollback, and give it longer than one business cycle.
- When a rule turns out to protect a failure path, write that reason in the rule's comment so the next cleanup does not ask again.

A clean firewall policy is worth the effort. The goal is to make it smaller without quietly removing the parts that only matter on a bad day.

Related reading: [rehearsing an ACL change against every flow]({{< ref "one-deny-line-289-flows-rehearse-the-change.md" >}}) and [a certificate rotation that broke TLS inspection]({{< ref "certificate-rotation-breaks-tls-inspection.md" >}}). More in the [change rehearsal guide](/change-rehearsal/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
