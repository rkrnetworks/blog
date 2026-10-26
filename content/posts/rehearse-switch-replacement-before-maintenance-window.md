---
title: "Swapping a floor switch at 2 AM? Rehearse it before the maintenance window"
date: 2026-10-29
description: "A switch replacement checklist covers the steps, not the impact. Rehearse the swap on a synthetic twin to see which hosts, APs and Wi-Fi users get hit."
tags: ["change management", "maintenance window", "switch replacement", "blast radius", "Wi-Fi", "synthetic twin"]
slug: "rehearse-switch-replacement-before-maintenance-window"
cover:
  image: "/covers/rehearse-switch-replacement-before-maintenance-window.jpg"
  alt: "Swapping a floor switch at 2 AM? Rehearse it before the maintenance window (cover image)"
  hiddenInSingle: false
audio: ["/audio/rehearse-switch-replacement-before-maintenance-window.mp3"]
audioDuration: "6:07"
---

Tonight at 02:00 the floor 7 switch gets replaced. It's a routine job. The new switch is staged, the config has been checked, and the change request is approved. Everyone involved would still like to know one thing before they start: who actually loses connectivity, and for how long?

## How network teams usually plan a switch swap

Ask on any network forum how people handle a physical switch replacement and the answers are thorough. Rack the new switch next to the old one. Match the config as closely as possible and check it twice. Back up both. Label every cable that's still in use. Move one cable at a time during the window, then verify that traffic is passing and downstream hosts are reachable. Keep the old switch powered for a while in case you need to roll back.

All of that is good practice, and none of it changes. But look at what the checklist covers. It's about doing the swap carefully. It doesn't say much about the impact of the swap: which wired hosts lose their gateway while the switch is out, which access points lose their uplink, and which Wi-Fi users can roam to a neighbour and which can't.

That part is usually worked out from spreadsheets, diagrams and memory. Then the change is pushed and the network gives the real answer. If something was missed, it turns up in production, on a bridge call, after hours, with more people than anyone planned for.

## Rehearse the change on a synthetic twin first

The demo below runs the same change on a synthetic twin of a made-up 12-floor building, from one CLI session. The building has 14 switches, 65 access points, 280 wireless clients and 272 wired hosts. The switch being replaced is R7-SW01, on floor 7, which has 7 access points and 18 Wi-Fi devices.

{{< youtube bl9P8cb5VHA >}}

It starts with a preview, with nothing applied. SETU predicts that during the swap 48 ports go dark, 22 wired hosts lose their gateway, and 7 APs lose their uplink.

The next question is the one that tends to cause surprises: what happens to Wi-Fi? Of the 18 devices on floor 7, 16 roam to neighbouring APs. Two would be stranded in a coverage hole. That changes the plan in a small, concrete way: bring a temporary AP for those two.

Then it's written down. The impact goes into a PDF report, ready to attach to the change request, so the change board sees the blast radius before anyone touches the switch.

After that comes the rehearsal itself. A point on the timeline is marked, and the switch is failed in the model. The outage spreads across floor 7 just as the preview said. The twin also flags that the same failure pattern has been seen before, which is worth knowing when deciding how careful to be.

Finally, it goes back to the marked point. Everything is restored, the hosts get their gateway back, and every AP comes back on air.

The numbers from this take: the full impact of losing the floor 7 switch was worked out in 168 ms. 16 of 18 guest devices stay online, 2 devices were found without Wi-Fi before the change rather than during it, it took 30 seconds to rehearse the change and undo it, and no guests were touched.

## What the rehearsal changes

The swap itself doesn't change. The difference is that the team walks into the window knowing who gets hit.

That has practical effects. The two users who would have lost Wi-Fi get a temporary AP instead of a complaint the next morning. The 22 wired hosts that lose their gateway can be warned, or their owners told when to expect it. The change board gets an impact report it can actually read, rather than a line saying "low risk, brief outage expected." And fewer people need to sit on the bridge, because fewer things are going to be a surprise.

It also makes rollback decisions easier. If something during the real swap doesn't match the preview, that's a clear signal to stop and look, not a judgement call made at 2:30 AM.

SETU works alongside the Cisco, Aruba, Juniper and Arista gear you already run. RKR doesn't sell hardware.

Outages and risky changes don't keep business hours, and neither does anyone probing your network for weak spots. Attackers practice. Your engineers should too.

## Practical takeaways

- Keep your switch replacement checklist. Add one step before it: preview the impact, with nothing applied.
- Look at Wi-Fi separately from wired. Wired impact is usually obvious from the port map. Who gets stranded on Wi-Fi is not, and it's where the surprises come from.
- Turn every stranded user into a line in the plan, whether that's a temporary AP, a notice, or a different window.
- Attach the impact report to the change request. A change board that can see the blast radius has much less to guess about.
- Rehearse the failure and the rollback, not just the change. Being able to fail the switch in the model and put it back in seconds means you can try the awkward cases too.
- Check whether the same failure pattern has happened before. History is a cheap way to calibrate how cautious to be.

For a wider tour of what a twin can do on a smaller site, including two switches failing at once, see [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}). If the switch you're replacing is old and out of support, the next post covers [planning an end-of-support refresh by impact]({{< ref "end-of-support-network-refresh-planning.md" >}}).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
