---
title: "Sticky clients: why laptops hold on to a far access point"
date: 2026-10-29T10:00:00+05:30
description: "A laptop sits under a strong access point but stays connected to a weak one across the floor. Sticky clients are a client decision, shaped by the network. A synthetic twin shows where they happen and which settings help."
tags: ["Wi-Fi", "roaming", "wireless design", "sticky clients", "synthetic twin", "RKR SETU"]
slug: "sticky-wifi-clients-wont-roam"
audio: ["/audio/sticky-wifi-clients-wont-roam.mp3"]
audioDuration: "4:15"
cover:
  image: "/covers/sticky-wifi-clients-wont-roam.jpg"
  alt: "Sticky clients: why laptops hold on to a far access point (cover image)"
  hiddenInSingle: false
---

A user walks from a meeting room at one end of the floor to their desk at the other. Their laptop still shows three bars, but pages load slowly and the next call is choppy. Looking at the controller, the laptop is still connected to the access point in the meeting room, thirty meters away, while an access point directly above their desk has almost nobody on it.

This is a sticky client, and it is one of the most common Wi-Fi complaints in any office.

## The client decides, not the network

In Wi-Fi, the client chooses when to roam. The access points can suggest, steer and nudge, but the decision to leave one and join another belongs to the laptop, phone or scanner. Each device family makes that decision differently. Some roam as soon as the signal drops a little. Others hold on until the connection is nearly unusable.

From the client's point of view, holding on makes sense. Roaming costs a short interruption, and the signal is still above whatever threshold its driver uses. From the user's point of view, it is a slow connection at a desk that should have perfect Wi-Fi.

## What the network does to make it worse

Access points running at high transmit power make far access points look better than they are. The client hears the distant access point clearly enough, so it sees no reason to move, even though the access point can barely hear the client in return. Low data rates enabled for compatibility give that weak connection somewhere to fall back to, instead of forcing a roam.

There is also the layout. Long open floors with glass meeting rooms let signal travel a long way. A client that associates in one corner can keep a usable link to that corner from almost anywhere.

## Following one laptop across a made-up floor

Consider an illustrative office floor with 14 access points and a mix of laptops and phones. The synthetic twin models the floor, the walls, the access points and their settings, and the way a typical laptop decides when to roam.

Walking a laptop from the north meeting room to a desk on the south side, the twin shows the client staying on the meeting room access point for most of the walk. The signal it sees stays above its roaming threshold until very close to the south wall. Along the way, the data rate it can use drops to a fraction of what the closer access point would give.

Now change two things in the twin: reduce transmit power on the access points along the open side of the floor, and disable the lowest data rates. Walk the same route again. The laptop roams twice along the way, ends up on the access point above the desk, and keeps a much better rate throughout.

The twin also shows the cost of those changes. With lower power, one corner near the stairwell drops close to the edge of coverage. That is worth knowing before the change goes out, and it suggests one extra access point or a small move rather than a settings rollback.

## A practical approach to sticky clients

- Start by finding where they happen. Clients that stay connected at low signal for a long time point to specific areas.
- Bring transmit power down to what the floor needs, and match it roughly to what typical clients transmit.
- Remove the lowest data rates where every client supports better ones.
- Use roaming assistance features carefully, and test them with the actual devices on the floor.
- Check coverage at the edges after any power change, especially in stairwells and corners.
- Remember that one device type may behave very differently from the rest. Test with the ones your users carry.

Sticky clients will never fully go away, because the decision is not yours. But the network can make the right decision much easier for the client to reach.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
