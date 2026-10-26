---
title: "A packet can arrive and still be late: testing QoS in a synthetic twin"
date: 2026-11-08
description: "A call connects, the audio packets arrive, and they still miss their deadline. Following one packet hop by hop, then testing three QoS policies from exactly the same state in a synthetic twin."
tags: ["QoS", "voice and video", "network performance", "change management", "queuing", "synthetic twin", "RKR SETU"]
slug: "qos-packet-arrives-still-late"
audio: ["/audio/qos-packet-arrives-still-late.mp3"]
audioDuration: "3:58"
cover:
  image: "/covers/qos-packet-arrives-still-late.jpg"
  alt: "A packet can arrive and still be late: testing QoS in a synthetic twin (cover image)"
  hiddenInSingle: false
---

A packet can arrive and still miss its deadline.

That's the hard part of real-time traffic. A call connects, nothing is dropped, every packet makes it across the network, and the audio still breaks up. From a reachability point of view the network is working. From the caller's point of view it isn't.

## Why QoS problems are hard to pin down

Voice and video don't just need their packets to arrive. They need them to arrive in time. When audio, video and background traffic all share the same links, the difference between a good call and a bad one is which queue each packet lands in and how long it waits there.

Those problems also tend to come and go. They depend on what else is on the link at that moment. So the usual approach is to change a policy, wait for the problem to come back, and see if it's better. That can take days, and it's hard to know whether a good afternoon was the fix or just a quiet one.

## Following one call in a synthetic twin

The video below follows a call across a made-up network in a synthetic twin.

{{< youtube lZecHSyKano >}}

Watch it on YouTube: https://youtu.be/lZecHSyKano

There's a caller on one side of the estate and a peer on the other. The call goes out through the access switch and across the network. Each packet carries its own headers and its own deadline, 65 milliseconds in this example. Audio, video and background traffic all share the same links.

On port 47, nothing is trusted. Every packet lands in the same default queue, on a port serialising at 256 kilobits per second. So audio waits its turn, hop by hop. It still arrives. Just late.

The declared limits for the workload are clear: no more than 5 percent of audio packets missing their deadline, no more than 10 percent of video, and at least 64 kilobits per second left for background traffic.

Then the policy is changed, and each attempt is tested from exactly the same state.

First attempt: send everything to the voice queue. Twenty in a hundred audio packets still miss their deadline, and video misses 9 of 17. The limits aren't met.

Next, trust the markings. Audio is clean, with no misses in a hundred, but video still misses 4 of 17. Closer, and still not met.

Then video joins the voice queue, and the test runs again from the same state. This time audio misses none and video misses none. Every declared limit is met.

## Why the same state matters

The useful thing here isn't any one policy. It's that all three were tested against the same traffic, at the same moment, on the same network. That turns QoS from a matter of opinion into a comparison. The first attempt sounds sensible and fails. The second fixes audio and leaves video short. Only the third meets every limit.

Without a way to rerun the same state, each of those would have been a change in production, followed by a wait to see what happened.

## Practical takeaways

- Write down the limits before you tune anything: how many late packets each class can tolerate, and how much the background traffic needs.
- Check trust settings at the edge. A port that trusts nothing puts every packet in the same queue.
- Measure deadlines, not only delivery. A packet that arrives late is a lost packet to a voice call.
- Compare policies against the same state, so the result reflects the policy and not the time of day.
- Keep the version that meets every limit, and the record of the ones that didn't.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
