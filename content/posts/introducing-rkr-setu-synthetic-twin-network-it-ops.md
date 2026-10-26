---
title: "Introducing RKR SETU 1.0: one synthetic twin for network and IT operations"
date: 2026-11-01
description: "One ticket or a thousand, each one starts somewhere in the network. A walk through RKR SETU 1.0 on a made-up site: the fault, the moments before it, what-if questions, Wi-Fi, security policy and the wider estate."
tags: ["network operations", "IT operations", "root cause analysis", "blast radius", "change management", "synthetic twin", "RKR SETU"]
slug: "introducing-rkr-setu-synthetic-twin-network-it-ops"
audio: ["/audio/introducing-rkr-setu-synthetic-twin-network-it-ops.mp3"]
audioDuration: "4:10"
cover:
  image: "/covers/introducing-rkr-setu-synthetic-twin-network-it-ops.jpg"
  alt: "Introducing RKR SETU 1.0: one synthetic twin for network and IT operations (cover image)"
  hiddenInSingle: false
---

Whether it's one ticket or a thousand, each one starts somewhere in the network. A floor loses its connection, a call breaks up, a change goes in and something quietly stops working. The people who pick up those tickets, in TAC, the NOC, the SOC, at a managed service provider or in professional services, all end up asking the same few questions. What broke, who is affected, what happened just before, and what happens if we change something?

This post introduces RKR SETU 1.0 and walks through the short video we made to show it.

## How this usually goes

Most teams answer those questions with a mix of tools. One shows the switches, another shows the access points, a third shows security policy, and the virtual machines and the wide area network live somewhere else again. A diagram helps, if it's current. Someone who knows the site helps more, if they're on shift.

So the first part of almost every incident is assembly. Pulling the pieces together, lining up what each tool says, and working out how they connect. The fix is often small. Getting to it is what takes the time.

## One site, end to end, in a synthetic twin

SETU works from a synthetic twin: a model of the building, its floors and everything connected to them, in one place. The video below is a tour of a made-up site, not a customer network.

{{< youtube 0XEbW-W8Zvo >}}

Watch it on YouTube: https://youtu.be/0XEbW-W8Zvo

A ticket comes in: no network on the first floor ward. In the twin, ten access points are down and thirty clients are affected. The trail leads to one access switch, with ten ports down.

From there the video shows the kinds of questions the twin can answer. It can go back in time, to the moments before the failure, so you can see the state of the site before anyone noticed a problem. It can ask what if. Lose one uplink, then a second, and see exactly who is affected each time.

It can walk the floor point by point and measure the wireless signal, and show where coverage reaches its edge. It can follow a single wireless client to the access point serving it. It can check security policy along the path, through the racks and into the core, and show exactly where a flow is denied and dropped.

It goes down into virtualisation, the hosts and the six machines running on them in this example, and out across the estate, thirty-nine sites joined over the wide area network.

The point isn't any one of those views. It's that they all sit in the same model, so moving from a ticket to a switch to a policy to a host doesn't mean switching tools or guessing how they connect.

## What we mean by "for all"

We build synthetic twins for all. By all, we mean switching, routing, wireless, firewalls and security, data centers, power and cooling, and compute. Campus to cloud, one synthetic twin.

That also means the network you actually have, not only the newest part of it. Older and mixed devices belong in the same model, as we explain in [too old for the cloud?]({{< ref "cloud-management-for-old-and-mixed-network-devices.md" >}}).

## Practical takeaways

- Count how many tools your team opens before it can say what a ticket affects. That number is a good measure of how much time goes into assembly rather than fixing.
- Ask for the blast radius before the change, not after it. Which floors, which access points, how many clients.
- Keep the moments before a failure. The state just before a fault is often the fastest way to its cause.
- Treat security policy, virtualisation and the wide area network as part of the same path, because to the user they are.

If you're new to the idea, start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}).

We build synthetic twins for all.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
