---
title: "Video calls drop in one meeting room: find the cause, fix it, prove it"
date: 2026-10-29T12:00:00Z
draft: true
description: "Every AP is up, but video calls keep dropping in one meeting room. A synthetic twin finds the gap, previews the fix, then fails the closet switch to prove it."
seoTitle: "Video calls drop in one meeting room: find, fix, prove"
tags: ["Wi-Fi troubleshooting", "wireless design", "voice over Wi-Fi", "Wi-Fi", "roaming", "coverage planning", "DFS", "change management", "root cause analysis", "synthetic twin", "RKR SETU"]
categories: ["Wi-Fi", "RKR SETU", "Change rehearsal"]
keywords: ["video calls dropping in meeting room", "Wi-Fi coverage gap", "voice over Wi-Fi validation", "Wi-Fi troubleshooting", "AP transmit power change", "DFS radar event", "closet switch failure", "synthetic twin", "RKR SETU"]
slug: "video-calls-drop-meeting-room-find-fix-prove"
audio: ["/audio/video-calls-drop-meeting-room-find-fix-prove.mp3"]
audioDuration: "5:56"
videoDuration: "PT11M48S"
cover:
  image: "/covers/video-calls-drop-meeting-room-find-fix-prove.jpg"
  alt: "Video calls drop in one meeting room: find the cause, fix it, prove it (cover image)"
  hiddenInSingle: false
# Video: Wi-Fi long-form, cut 3 (11:48). YouTube ID VIDEO_ID.
---

It's 11:00 on a Tuesday. The ticket says video calls keep dropping in the floor-9 meeting room. You check the wireless side and everything looks healthy: all 219 access points joined, every client counted. On paper, nothing is wrong.

Most Wi-Fi teams know this ticket. It's never a full outage. It's one room, at certain times, for certain people, and it's very hard to reproduce once someone walks in with a laptop.

Our new film follows this ticket from start to finish in RKR SETU 1.0, inside a synthetic twin of a made-up two-tower office at peak: 3,555 people and 8,891 devices. The office is invented, and every figure in the film was computed in the synthetic twin in this take. Nothing here is measured from a live site.

{{< youtube VIDEO_ID >}}

Watch it on YouTube: https://youtu.be/VIDEO_ID

## Design first, then validate against voice

The film starts before the ticket exists. Floor 9 is designed in the synthetic twin: twenty access points, the antennas they use, the interference around them and the furniture in the rooms. Couches, tables and people all change how a room behaves for a radio. If interference is your usual suspect, we looked at that on its own in [39 radios, 2 channels]({{< ref "wifi-interference-39-radios-two-channels.md" >}}).

Then the design is checked against voice, the hardest everyday job on Wi-Fi. A good-looking heatmap is not the same as a good call. Voice needs a strong signal, a quiet noise floor and a second access point ready for the roam.

The sharper question is what the phone in a caller's hand actually gets, at about 1.2 m off the floor. Checked that way, 48 rooms have some area below the floor, and the meeting rooms are at the top of the list, the floor-9 one among them. On a design review that's a note. In real life it becomes the ticket above.

## Find the cause, not just a cause

There are three usual suspects for dropped calls in one room:

- Coverage: the signal at the table is too weak.
- Contention: too many devices on one channel.
- Roaming: the handover between access points is slow or lands badly.

In the film, the twin checks each one. Contention isn't it. The roam is quick, about 21 ms. The cause is coverage: a gap at about -105 dBm inside the meeting room, called F9-G1, 11 m from the nearest access point. Two suspects are ruled out before anyone walks to the room.

Roaming is often the first thing people blame. When it really is the roam, it looks different, as in [sticky clients that hold on to a far access point]({{< ref "sticky-wifi-clients-wont-roam.md" >}}) and [the 42 ms service gap on a robot]({{< ref "robot-wifi-roaming-42-ms-service-gap.md" >}}).

## Preview the fix before you make it

Next, the possible fixes are ranked, from the one that helps most to the ones that change nothing. The best option is to raise one access point, AP-01, from 17 to 23 dBm.

Before applying it, the change is previewed: who else does this touch? The answer is 14 clients out of 993 moving to a different access point. Everyone else stays put. That's a change you can explain to a change board in one sentence. It's the same habit we described in [one deny line, 289 flows blocked]({{< ref "one-deny-line-289-flows-rehearse-the-change.md" >}}): see what a change does before the window, not after.

Then it's applied and re-checked. The gap in the room is gone.

## Then break it on purpose

A fix that only works on a calm day isn't finished. So the film stresses it twice.

First a radar event hits a floor-9 channel. Under DFS rules that access point has to leave the channel within 10 seconds. Every associated client is dropped and has to find its way back, and the access point moves to a clear channel.

Then the floor-9 closet switch fails. Ten access points lose their uplink and wired hosts lose their gateway. 377 clients roam and stay online. 37 more roam but land below the SLA, and you can see exactly which ones and where they sit, long before this happens for real. For the wired side of the same kind of failure, see [how Wi-Fi drops trace back to one switch]({{< ref "wifi-keeps-dropping-trace-to-one-switch.md" >}}) and [rehearsing a switch replacement before the window]({{< ref "rehearse-switch-replacement-before-maintenance-window.md" >}}).

## The proof

The film ends with the two things a change board actually wants: the change record (AP-01, 17 to 23 dBm, who, what and why) and the blast report for the closet switch failure, listing every affected client and what happens to it.

## A checklist for your next "calls drop in one room" ticket

- Check coverage at the height people hold phones, not only at ceiling height.
- Rule out contention and roaming with evidence, not instinct.
- Rank more than one fix, and know who each one moves before you apply it.
- Re-check after the change, then fail the nearest closet switch in the synthetic twin and see who is left behind.
- Keep the change record and the blast report together, so the next person knows why the change was made.

New to the idea? Start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}), or read [the RKR SETU 1.0 introduction]({{< ref "introducing-rkr-setu-synthetic-twin-network-it-ops.md" >}}). Moving to 6 GHz next? [Here's where the new coverage holes show up]({{< ref "six-ghz-rollout-new-coverage-holes.md" >}}).

Break it here first. Fix it here first.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
