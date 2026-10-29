---
title: "A new access switch became spanning tree root: why the whole floor went slow"
date: 2026-10-29T10:00:00+05:30
description: "A switch added to a quiet corner of the building takes over as spanning tree root, and traffic for a whole floor starts taking the long way. Here is how to see it before it happens."
tags: ["spanning tree", "switching", "layer 2", "change management", "synthetic twin", "RKR SETU"]
slug: "new-switch-becomes-spanning-tree-root"
audio: ["/audio/new-switch-becomes-spanning-tree-root.mp3"]
audioDuration: "4:03"
cover:
  image: "/covers/new-switch-becomes-spanning-tree-root.jpg"
  alt: "A new access switch became spanning tree root: why the whole floor went slow (cover image)"
  hiddenInSingle: false
---

Someone needed four more ports in a meeting room, so a small switch went in under the table. It came out of the box with default settings. By lunchtime, half the third floor was complaining that file transfers crawled and video calls stuttered, and nobody connected the two events.

The new switch had the lowest bridge ID on the network. Spanning tree did exactly what it was designed to do and elected it root. Every other switch then recalculated its best path toward a box sitting on a single 1 gig uplink in a meeting room.

## How a small switch takes over

Spanning tree picks a root bridge by priority first and MAC address second. If nobody set the priority on the core switches, every switch shares the same default, and the lowest MAC address wins. New hardware does not always have a higher address than the old core, and switches pulled from a spare shelf can have very low ones.

Once the root moves, the tree is rebuilt around it. Links that used to forward start blocking, and links that used to block start forwarding. Traffic between two floors may now go down to the meeting room and back up again. Nothing is broken. Every port is green. It is just slow, in a way that is hard to explain from any single device.

## Why it is hard to catch in a review

The change that caused this was not a network change at all. It was a facilities request for more ports. No one reviewed the spanning tree priority of a small switch nobody thought twice about.

Even when engineers do look, the answer depends on the whole topology. Which switch would win an election, and which ports would block afterward, depends on every bridge ID and every path cost. That is easy to state and tedious to work out by hand.

## Seeing the election before it happens

Picture a made-up office: one core pair, eight access switches across four floors, and a few small switches people have added over the years. In a synthetic twin of that office, adding a new switch to a meeting room port is a single step.

The twin shows the result straight away. The new switch would become root. Six uplinks would change state. Traffic from floor two to the server room would now detour through the third-floor access switch the meeting room switch hangs off, and that access switch's uplinks would carry several times the load they were built for.

Then the fix can be checked the same way. Set the core switches to the lowest priority, set root guard on access ports facing users, and add the meeting room switch again. This time the root stays where it belongs, and nothing else moves.

That second run is the useful one. It turns a rule everyone knows they should follow into a demonstration of what happens when they do not.

## Habits that keep the root where it belongs

- Set spanning tree priority explicitly on the core switches, with a clear primary and secondary root.
- Turn on root guard on ports that should never lead toward the root, such as user-facing access ports.
- Use BPDU guard on edge ports so an unexpected switch shuts the port rather than joining the tree.
- Keep a short list of small switches that exist outside the closets, and who owns them.
- After any change, check which bridge is root, not just whether links are up.
- When a whole floor goes slow at once with nothing down, look at the tree before you look at the applications.

Spanning tree problems often look like application problems, because the network keeps working, only worse. Knowing where the root is, and where it would move, takes most of the mystery out of them.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
