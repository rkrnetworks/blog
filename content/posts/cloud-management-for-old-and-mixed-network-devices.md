---
title: "Too old for the cloud? Old and mixed network devices still belong in one synthetic twin"
date: 2026-10-26T05:00:00Z
description: "Vendor cloud management focuses on newer, supported gear from one maker. SETU works the other way around: old, mixed and end-of-support devices go into one synthetic twin."
tags: ["synthetic twin", "RKR SETU", "cloud management", "end of life", "multi-vendor network", "network refresh planning"]
slug: "cloud-management-for-old-and-mixed-network-devices"
cover:
  image: "/covers/cloud-management-for-old-and-mixed-network-devices.jpg"
  alt: "Too old for the cloud? Old and mixed network devices still belong in one synthetic twin (cover image)"
  hiddenInSingle: false
audio: ["/audio/cloud-management-for-old-and-mixed-network-devices.mp3"]
audioDuration: "5:01"
seoTitle: "Old and mixed network devices in one synthetic twin"
seoDescription: "Vendor cloud management favours new, supported gear from one maker. Old, mixed and end-of-support devices still belong in one synthetic twin of the network."
categories: ["RKR SETU"]
---

Most cloud management only works with newer gear from one vendor. SETU works the other way around. If a device is too old for a vendor's cloud, we still bring it into SETU. Twenty years old? Still in SETU. Mixed brands, end-of-support, never cloud-ready? All of it goes into one synthetic twin, so your whole network shows up, not just the newest part of it.

We build synthetic twins for all. This post explains what we mean by that, and just as importantly, what we don't.

## What vendor clouds are built for

Cisco Meraki, HPE Aruba Central and Arista CloudVision are each built around their own maker's hardware. They focus on newer, supported models, and that makes sense. A vendor can do the most with gear it designed and still supports, and many teams run those platforms well.

The catch is that very few networks are made of one vendor's current models. A typical building has a core switch from one era, access switches from another, access points from two or three generations, and a closet or two of gear nobody has touched since it was installed. Some of it came with an acquisition. Some of it was never designed for cloud management in the first place. Some of it is past its maker's support, still running, still carrying traffic.

So the cloud view ends up showing the newest part of the network. The older part, often the part everything else depends on, lives in spreadsheets, old diagrams and someone's memory.

## What SETU does differently

SETU starts from the network you actually have. The device doesn't need to be cloud-ready, current, or from a particular maker. If it's in your building and carrying traffic, it belongs in the model.

That's what we mean by "for all". Old and new, supported or not, every device sits in the same synthetic twin and is modelled and tested the same way. A 2006 switch and a Wi-Fi 6E access point show up side by side, with the cables, floors, closets and power that connect them.

We want to be careful with the word "support" here. When we say a device is supported in SETU, we mean it's modelled inside the synthetic twin. We don't mean vendor support, firmware updates, repairs or replacement parts. Those still come from the maker or your maintenance provider, and RKR doesn't sell hardware. We also won't claim every device ever made is already covered. If you have something unusual, ask us, and we'll tell you honestly where it stands.

## Why the old gear matters most

It's tempting to think the old devices are the least interesting part of the network. In practice they're often the most important part to understand.

An old core switch can carry a whole tower. A closet switch past its support date can be the only path for a floor's access points. A subnet behind an old router may have no standby gateway at all. When something fails, it's rarely the newest box that surprises people.

With all of it in one synthetic twin, the questions get specific answers. What goes dark if that 2011 core fails tonight? Which floors lose Wi-Fi if an old closet switch is pulled during a refresh? Which end-of-support devices should be replaced first, by what they carry rather than by age? Our [refresh planning example]({{< ref "end-of-support-network-refresh-planning.md" >}}) works through exactly that on a made-up building where 44 of 98 devices are past their maker's support.

## Where this leaves your vendor cloud

SETU isn't asking you to give up a vendor platform you're happy with. If your newest gear is managed in a vendor's cloud, that can stay as it is. What SETU adds is one place where the whole estate shows up together, including the parts that a single-vendor view leaves out, so you can rehearse changes and failures against all of it.

It also means older gear doesn't have to be replaced just to become visible. You can keep running what still works, see what it carries, and plan the refresh on your own schedule.

## Practical takeaways

- List the devices your current management tools don't show. That list is usually longer than people expect, and it tends to include the core.
- Don't judge old gear by age alone. Judge it by what fails with it.
- Keep vendor support and modelling separate in your head. A device can be out of its maker's support and still be fully understood in your planning.
- Plan refreshes against the whole network, old and new together, not just the part that is easiest to see.

If you're new to the idea, start with [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}).

Related reading: [replacing the right things first]({{< ref "rkr-podcast-ep02-replace-the-right-things-first.md" >}}). More in the [RKR SETU overview](/setu/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
