---
title: "Data center planning and operations: power, cooling, space and the network"
seoTitle: "Data center guide: power, cooling, cable trays and GPU clusters"
description: "How power, cooling, space, cabling and the network depend on each other in a data hall, and every data center post on the blog in one place."
seoDescription: "A data hall rated N+1 can still overheat, trip a breaker or run out of tray space. A guide to how power, cooling, space and network interact in practice."
url: "/data-center/"
layout: "hub"
hubCategory: "Data center"
breadcrumb: "Data center"
date: 2026-10-29
hiddenInRss: true
cover:
  image: "/images/hubs/data-center.jpg"
  alt: "Data center planning and operations guide from RKR Networks"
---

A data center is several systems that have to agree with each other: space, power, cooling, cabling and the network. Each has its own team, its own drawings and its own idea of spare capacity. Most surprises happen where they meet: a rack that is fine on power but hot on air, a row that fits on the floor plan but not in the cable tray, a GPU job that stops because one switch failed. This guide walks through those seams and links every data center post on the blog.

## Power: redundancy you can count, and the parts you can't

Data center power is usually described with letters: **N** is the capacity the load needs, **N+1** adds one spare unit, **2N** duplicates the whole path. Behind the letters sit utility feeds, generators, an **ATS** (automatic transfer switch), **UPS** systems, busway or switchboards, and rack **PDUs**.

Things that catch teams out:

- **The gap during transfer.** When the utility fails, the generator needs seconds to take over. Anything not on a UPS reboots. See [which systems reboot in a generator transfer test]({{< ref "posts/generator-transfer-test-what-reboots.md" >}}).
- **Phase balance.** A three-phase PDU can look half empty and still trip a breaker if one phase carries most of the load. See [PDU phase imbalance]({{< ref "posts/pdu-phase-imbalance-trips-rack-breaker.md" >}}).
- **Maintenance uses up redundancy.** With one busway or UPS out for work, a 2N design is temporarily N. A second fault then matters a lot. See [rehearsing busway maintenance and the second fault]({{< ref "posts/rehearse-maintenance-second-fault.md" >}}).

## Cooling: capacity is not the same as airflow

A hall can have enough cooling capacity on paper and still have hot racks. Cooling units (**CRAC** or **CRAH**) deliver cold air; containment keeps it from mixing with the hot exhaust. Load placement, blanking panels, floor tiles and gaps in containment decide where the air actually goes.

- **N+1 that isn't.** Losing one cooling unit can matter if the remaining units cannot reach the racks that need them. See [whether the room is really N+1]({{< ref "posts/crac-unit-fails-is-the-room-really-n-plus-one.md" >}}).
- **Containment gaps.** A missing door or panel at the end of a row lets hot air recirculate into the last few racks. See [why three racks run hot]({{< ref "posts/hot-aisle-containment-gap-three-hot-racks.md" >}}).

## Space and cabling: the overlooked constraint

New rows are planned for floor space, power and cooling. The overhead **cable tray** that has to carry their fibre and copper is often checked last. Tray fill along the whole route, not just at the new row, decides whether the cables fit. See [checking cable tray fill before adding a row]({{< ref "posts/cable-tray-fill-before-adding-a-row.md" >}}). For a full build, from pedestals and raised floor to pipework, see [a data center build-out on one page]({{< ref "posts/data-center-build-out-one-team-one-page.md" >}}).

## The network inside the hall

In a modern hall the network is a **leaf-spine** fabric: each rack has one or two **top-of-rack (ToR)** switches connected to every spine. For AI and HPC workloads, a training job is spread across many GPUs in many racks, and it waits for the slowest member. That means one ToR failure can pause far more work than the servers it connects. See [one ToR switch failing in a GPU cluster]({{< ref "posts/gpu-cluster-one-tor-switch-fails.md" >}}).

The hall also carries traffic from the rest of the estate. A DHCP reply, an authentication request or a routing update often crosses it. Problems that show up as office Wi-Fi tickets can end in a data hall.

## Operations: incidents rarely stay in one layer

A fibre trunk cut, a leak under the floor, stale sensors and flapping ports: real incidents mix facilities and network. See [15 data center incidents in one synthetic twin]({{< ref "posts/fifteen-data-center-incidents-build-run-manage.md" >}}).

Looking further ahead, halls were laid out for people with carts and ladders. If robots are to rack, stack and cable, aisle width, tray height and access matter in new ways. See [humanoid robots in the data hall]({{< ref "posts/humanoid-robots-aisle-width-cable-trays.md" >}}).

## Why one model for all of it

Because the failures happen at the seams, the most useful view puts space, power, cooling, cabling and the network in one model. A synthetic twin of the hall lets you trip a breaker, fail a cooling unit or remove a switch and see the effect on racks, servers and jobs together, then rewind and try the fix. The posts below each work one problem through on a made-up hall.

Terms like ATS, PDU, N+1 and ToR are explained in the [glossary](/glossary/). For failures beyond the hall, see the [outages and failover guide](/outages-and-failover/).
