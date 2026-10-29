---
title: "One top-of-rack switch fails in a GPU cluster: how many training jobs stop?"
date: 2026-10-29T10:00:00+05:30
description: "In a GPU cluster, one switch failure can stop far more work than the servers it connects. A synthetic twin of a made-up cluster shows how jobs spread across racks turn a single failure into a wide pause."
tags: ["GPU cluster", "AI infrastructure", "top of rack", "compute", "network design", "blast radius", "synthetic twin", "RKR SETU"]
slug: "gpu-cluster-one-tor-switch-fails"
audio: ["/audio/gpu-cluster-one-tor-switch-fails.mp3"]
audioDuration: "4:06"
cover:
  image: "/covers/gpu-cluster-one-tor-switch-fails.jpg"
  alt: "One top-of-rack switch fails in a GPU cluster: how many training jobs stop? (cover image)"
  hiddenInSingle: false
seoTitle: "One ToR switch fails in a GPU cluster: how many jobs stop?"
seoDescription: "One top-of-rack switch fails in a GPU cluster and far more work stops than its servers carry. See how jobs spread across racks widen the pause, in a twin."
categories: ["Data center", "Outages and failover"]
---

In a traditional server room, a top-of-rack switch failure affects the servers in that rack. If they have dual connections, possibly nothing at all. In a GPU cluster running large training jobs, the same failure can pause work on hundreds of servers in racks that have nothing wrong with them.

The reason is how training jobs are laid out.

## Jobs that span racks

A large training job runs across many GPU servers at once, and those servers talk to each other constantly. If any one of them stops responding, the whole job waits, and after a timeout it usually fails back to its last checkpoint.

Schedulers place jobs wherever capacity is available, so a single job may use a few servers from many different racks. Lose one switch, and every job that had even one server in that rack is affected. A failure that touches a small fraction of the servers can stop a large share of the work.

Dual-homed servers help, but not always as much as expected. If the second connection goes to a different network that only carries storage or management traffic, the job's interconnect traffic still has nowhere to go.

## Why it is hard to answer quickly

The question "which jobs would stop if this switch failed" needs three things at once: the physical cabling of every server to every switch, the way the network carries job traffic between racks, and the current placement of every job. The first is in a cabling database. The second is in the network design. The third changes every hour.

So the answer usually arrives after the failure, in the form of a list of failed jobs.

## Running the failure in advance

Consider an illustrative cluster of 32 racks, each with eight GPU servers and its own top-of-rack switch. Each server has two network connections, one to its rack switch for job traffic and one to a separate network for storage.

With a typical mix of running jobs placed in the synthetic twin, failing the switch in rack 12 gives a clear result. Eight servers lose their job traffic path. But those eight servers belong to five different jobs, and those five jobs together use well over a hundred servers across 20 racks. All of them would stop.

From there, the twin makes it easy to compare options. One is cabling each server's job traffic to two switches instead of one. Another is a scheduler rule that keeps each job inside a smaller group of racks, so a single switch failure touches fewer jobs. A third is checkpointing more often, which does not prevent the stop but shortens the work lost.

In this example, the placement rule cuts the number of affected jobs sharply with no new hardware, and dual connections bring it close to zero. Each option has trade-offs, and seeing them side by side helps the network and scheduling teams agree.

## Questions worth asking about any GPU cluster

- For each switch, how many running jobs would stop if it failed, not just how many servers?
- Do servers have a second path for job traffic, or only for storage and management?
- Does the scheduler know about the network layout, or does it only see idle GPUs?
- How often are jobs checkpointed, and how much work is lost at a typical failure point?
- When a switch needs planned maintenance, can jobs be drained from its rack first?
- Are spare switches and optics close enough to make a swap fast?

Large clusters turn small failures into large pauses. The good news is that the size of that pause can be planned for, once you can see how the jobs and the network line up.

Related reading: [a 1,024-GPU job during power maintenance]({{< ref "rehearse-maintenance-second-fault.md" >}}), [a dual-homed server after a switch reboot]({{< ref "dual-homed-server-wrong-path-after-reboot.md" >}}) and [uneven LACP hashing]({{< ref "lacp-member-down-uneven-hashing.md" >}}). More in the [data center guide](/data-center/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
