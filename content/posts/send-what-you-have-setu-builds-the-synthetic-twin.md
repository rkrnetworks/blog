---
title: "No drawings? Send what you have. SETU builds the synthetic twin"
date: 2026-11-06T05:32:23Z
draft: false
description: "Onboarding a building with no drawings and no documentation: send site photos, an equipment list, configs and a headcount sheet, approve the build, and RKR SETU builds the synthetic twin, down to every rack, cable, desk and access point."
seoTitle: "No drawings? Onboard your network into a synthetic twin from the files you have"
seoDescription: "See how RKR SETU onboards a building with no drawings: send photos, an equipment list, configs and headcount, approve the build, and get a synthetic twin you can log in to and ping through."
tags: ["network onboarding", "network documentation", "equipment list", "switch configs", "access point", "CLI", "ping path", "synthetic twin", "RKR SETU"]
categories: ["RKR SETU"]
keywords: ["network onboarding", "no network drawings", "network documentation", "build a synthetic twin from configs", "equipment list to network model", "3D synthetic twin", "show clients", "LLDP neighbors", "ping path", "synthetic twin", "RKR SETU"]
slug: "send-what-you-have-setu-builds-the-synthetic-twin"
audio: ["/audio/send-what-you-have-setu-builds-the-synthetic-twin.mp3"]
audioDuration: "4:58"
videoDuration: "PT1M56S"
cover:
  image: "/covers/send-what-you-have-setu-builds-the-synthetic-twin.jpg"
  alt: "No drawings? Send what you have. SETU builds the synthetic twin (cover image)"
  hiddenInSingle: false
# Video: setu_onboarding, RKR SETU onboarding demo (1:56). YouTube ID: wlqra1eyYyA
---

No drawings. No documentation.

That's where a lot of networks start. The building has been running for years, the people who wired it have moved on, and what's left is a folder of photos, a spreadsheet of equipment, and the configs on the switches. In under two minutes, this demo shows RKR SETU taking exactly that and building a [synthetic twin](/glossary/#synthetic-twin) of the whole building.

{{< youtube wlqra1eyYyA >}}

Watch it on YouTube: https://youtu.be/wlqra1eyYyA

## Send what you have

There's one page, and you drop files anywhere on it. In the demo, the team behind a building called RKR-Corporate-7 sends what they keep:

- Eleven site photos: the aerial view, the entrance, the office floors, the equipment rooms, the ceiling.
- An equipment list.
- The configs from the switches, the core, the firewall and the WAN edge.
- A peak occupancy sheet: the headcount.

Every file shows up on the page with what SETU read out of it. The equipment list reads 414 facts from 414 of its 451 rows, and four columns SETU doesn't know yet are marked so you can say what they are. Each config shows how many facts came out of it. The headcount sheet reads all 10 of its rows.

The photos are kept with your files as a record of the site. They aren't read as a floor plan.

## Approve and build

When you're ready, you approve the build. In the demo, that's 1 site and 419 devices. Nothing is final: every part you add later becomes a new revision.

SETU also shows what it still doesn't know. Here, 11 parts of the estate are still open, such as where the site is and how many floors it has, and one site was worked out from the equipment rows. SETU asks you to type its real name.

## SETU builds the synthetic twin

Then the building appears in 3D, floor by floor.

Every rack and cable, mapped. The cable runs climb through the building to the equipment rooms. Every desk, every user, every access point on the ceiling.

Every device has its real name, the one from your own configs. Pick the access point RKR-C7-B1-F08-AP07, and its cable run shows 20.9 meters (69 feet) to switch RKR-C7-B1-F08-AS01, port Gi1/0/7.

## Log in to a device. It answers.

You can open a terminal on a device in the synthetic twin and ask it questions, the same way you would on the real one.

On that access point, `show clients` lists 15 wireless clients carried by 13 people: smartphones and a laptop on the corporate network, and an environment sensor on the IoT network, each with its address, VLAN and signal. `show lldp neighbors` finds its uplink: switch AS01, port Gi1/0/7, over cable C137. That's the same port the 3D view showed.

## Ping from a desk. See the exact path.

Then we sit down at a desk. On the laptop of one of those 13 people, `ipconfig` shows its address, 10.10.36.15, its mask and its gateway.

A ping to 10.10.32.1 comes back four for four, and the synthetic twin explains each step of the path. It compares the subnets and finds both addresses on the same /20 network. It decides no routing is needed, then asks over ARP who has the address. The answer is the VLAN 20 gateway interface, and the frame is switched straight across.

No guessing which way a packet goes. You see the exact path, step by step.

## Why it matters

Most teams don't skip documentation because they don't care. They skip it because drawing a building by hand takes weeks, and it's out of date the day it's done. Starting from the files you already have means the synthetic twin can start today, and it grows one revision at a time as you add more.

No matter how little you have, SETU builds the synthetic twin.

If you want the longer version of the idea, read [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}). To see what you can do once the twin is built, see [Yes, there's a GUI: try the fix in the synthetic twin first]({{< ref "yes-theres-a-gui-try-the-fix-in-the-synthetic-twin-first.md" >}}).

RKR-Corporate-7 is a made-up demo estate. All devices, people and addresses in it are simulated.

Book a demo with our team: sales@rkr-networks.com. In person or online.
