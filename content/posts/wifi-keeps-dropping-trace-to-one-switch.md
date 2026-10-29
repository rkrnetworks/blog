---
title: "Wi-Fi keeps dropping? Trace it to one switch, one floor down"
date: 2026-10-26T07:35:00Z
description: "A ticket says the Wi-Fi keeps dropping. In a synthetic twin, the red trail leads from seven access points and twenty-one offline users to one switch on the floor below, and rewinding shows the fault before anyone felt it."
tags: ["Wi-Fi troubleshooting", "access point", "access switch", "root cause analysis", "MTTR", "synthetic twin", "RKR SETU"]
slug: "wifi-keeps-dropping-trace-to-one-switch"
audio: ["/audio/wifi-keeps-dropping-trace-to-one-switch.mp3"]
audioDuration: "3:14"
cover:
  image: "/covers/wifi-keeps-dropping-trace-to-one-switch.jpg"
  alt: "Wi-Fi keeps dropping? Trace it to one switch, one floor down (cover image)"
  hiddenInSingle: false
seoTitle: "Wi-Fi keeps dropping? Trace it to one switch, one floor down"
seoDescription: "Wi-Fi keeps dropping and 21 users are offline. A synthetic twin follows seven access points to one switch on the floor below, then rewinds to the fault."
categories: ["Wi-Fi", "Outages and failover"]
---

"The Wi-Fi keeps dropping." It's probably the most common ticket in any building, and one of the least specific. Seven access points, twenty-one people offline, and the cause is one switch, one floor down. None of that is in the ticket.

## Why Wi-Fi tickets send people the wrong way

When users say the Wi-Fi is dropping, the natural place to look is the wireless. The access point near them, the channel, the signal. Sometimes that's where the problem is. Often it isn't. The access point is only the first thing to feel a problem that started somewhere else, in a switch, a cable or a power supply further up the path.

So the first part of the ticket is often spent proving the wireless is fine, before anyone looks at what the wireless depends on.

## Following the red trail in a synthetic twin

The video below follows the ticket through a synthetic twin of a made-up building. It's short, under a minute.

{{< youtube FfibVE28a58 >}}

Watch it on YouTube: https://youtu.be/FfibVE28a58

A ticket comes in. The Wi-Fi keeps dropping. The access point they mean is already red.

One click, and everything that Wi-Fi depends on lights up. One path is red. Follow it, and it ends at one switch, one floor down.

The Wi-Fi was the symptom. This box is the cause. Seven access points hang off it, and twenty-one people are offline right now.

Then the twin rewinds the incident. Before the fault, nothing was wrong yet. The Wi-Fi was just the first thing to feel it.

One action, and everything comes back. And the recovery is verified, not assumed.

One site, or ten thousand.

## What to take from it

The useful step in the video is the click that lights up everything the access point depends on. That's the step that skips the hour spent checking the wireless. Once the dependencies are visible, the red path is hard to miss, and the switch one floor down becomes the obvious place to look.

Rewinding is the other half. Seeing the building just before the fault answers the question that always comes up afterwards: was this the cause, or just something else that was broken at the same time? If the access points were fine until that switch failed, the answer is clear.

We wrote about a similar ticket that ended at one cable in [tracing the ticket to one cable]({{< ref "wifi-keeps-dropping-trace-ticket-to-one-cable.md" >}}). Different building, different cause, same habit: follow what the Wi-Fi depends on.

## Practical takeaways

- Treat "the Wi-Fi keeps dropping" as a symptom until proven otherwise.
- Look at everything the access point depends on, not just the access point: switch, uplink, cable and power.
- Count the impact in people, not only devices. Twenty-one people offline is a clearer message than seven access points down.
- Look at the state just before the fault to confirm the cause.
- Verify recovery after the fix, rather than waiting for the next ticket.

Related reading: [rehearsing a switch replacement]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}). More in the [Wi-Fi troubleshooting guide](/wifi/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
