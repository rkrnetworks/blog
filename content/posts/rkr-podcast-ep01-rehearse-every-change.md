---
title: "RKR Podcast, episode 1: rehearse every change before it goes live"
date: 2026-10-29T10:00:00Z
description: "A network lead sits in the customer's chair and questions an RKR technical marketing engineer about SETU 1.0. The idea running through the episode: rehearse every change on the synthetic twin before it goes live."
tags: ["podcast", "change management", "maintenance window", "single points of failure", "synthetic twin"]
slug: "rkr-podcast-ep01-rehearse-every-change"
audio: ["/audio/rkr-podcast-ep01-rehearse-every-change.mp3"]
audioDuration: "4:28"
cover:
  image: "/covers/rkr-podcast-ep01-rehearse-every-change.jpg"
  alt: "RKR Podcast, episode 1: rehearse every change before it goes live (cover image)"
  hiddenInSingle: false
# Podcast: RKR Networks Podcast, Episode 1. YouTube ID sVrDs5Qo_-E.
---

Tonight at 2 AM a switch gets replaced. The checklist is good. It says how to do the swap carefully. It says much less about what the swap will do.

That gap is where the first episode of the RKR Networks Podcast starts. A network lead sits in the customer's chair and asks the questions they'd ask in a real meeting. An RKR technical marketing engineer answers from what our SETU demos actually showed.

Everything discussed comes from recorded SETU demos run on made-up example sites. Both voices are AI-generated.

## Watch or listen

{{< youtube sVrDs5Qo_-E >}}

Prefer audio? The episode is also on the [RKR Podcast on Spotify](https://open.spotify.com/show/4uqMIzZcJCOMJ1utAEjNIJ). Every question, with its timestamp, is in the YouTube description.

## Why changes

Changes are where networks get hurt.

In Uptime Institute's Annual Outage Analysis 2026, configuration and change-management failure was the most-cited cause of major network outages. It was named by 41% of 122 operators who had a major network outage.

## The 2 AM switch swap

The episode opens on a made-up twelve-floor building. 14 switches, 65 access points, 280 wireless clients and 272 wired hosts. The switch being replaced is on floor 7.

The preview, with nothing applied, shows 48 ports going dark, 22 wired hosts losing connectivity and 7 access points losing their uplink.

The Wi-Fi is where the surprise is. Of the 18 devices on floor 7, 16 roam to neighbouring access points. 2 would be stranded in a coverage hole.

That changes the plan in a small, concrete way. Bring a temporary access point for those two.

Then the rehearsal. The switch is failed in the model, the outage spreads as the preview said, and the synthetic twin goes back to the marked point.

The full impact of losing that switch was worked out in 168 ms. Rehearsing the change and undoing it took 30 seconds in that demo.

If the real swap doesn't match the preview, that's a clear signal to stop and look.

## One failure, then two

On a made-up office floor with 3 switches, 16 access points and 56 cables, one switch fails. All 22 affected Wi-Fi clients roam. None are stranded.

Then two switches fail together. 6 clients go dark, and one subnet loses its gateway with no standby. That kind of double failure is hard to reason about on paper.

Failing it, checking it and undoing it took 31 seconds in that demo. No production devices were touched.

## What else the episode covers

- What happens when the model is wrong.
- The end-of-support refresh, as the way in.
- How SETU sits next to the tools and vendor AI a team already has.
- A floor 8 Wi-Fi ticket, traced to one cable.
- Six UPS alarms, and one rising main behind them.
- The second fault during planned maintenance.
- Security, voice quality, and tickets that bounce between teams.
- Who uses it, and what rollout looks like.
- A data hall, and robots on the warehouse floor.

## Practical takeaways

- Keep your swap checklist. Add the impact: who loses what, and who can roam.
- Preview first, then rehearse, then compare the real night against the preview.
- Test double failures, not just single ones.
- Keep a running list of single points of failure. Every scenario should add to it or cross something off.
- Give the change board the blast radius before anyone touches the switch.

For the written version of the switch swap, read how we [rehearse a switch replacement before the maintenance window]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}). For the bigger picture, start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}).

Rehearse every change on the synthetic twin before it goes live.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
