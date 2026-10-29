---
title: "One cooling unit fails: is the room really N+1?"
date: 2026-10-29T10:00:00+05:30
description: "A data hall is designed N+1 for cooling, and on paper one unit can fail without harm. In practice, airflow, load placement and maintenance can make one failure matter. A synthetic twin of a made-up hall shows how."
tags: ["cooling", "N+1", "data center", "power resilience", "capacity planning", "synthetic twin", "RKR SETU"]
slug: "crac-unit-fails-is-the-room-really-n-plus-one"
audio: ["/audio/crac-unit-fails-is-the-room-really-n-plus-one.mp3"]
audioDuration: "3:42"
cover:
  image: "/covers/crac-unit-fails-is-the-room-really-n-plus-one.jpg"
  alt: "One cooling unit fails: is the room really N+1? (cover image)"
  hiddenInSingle: false
seoTitle: "One CRAC unit fails: is your data hall really N+1?"
seoDescription: "A data hall rated N+1 for cooling should survive one unit failing. Airflow, load placement and maintenance can say otherwise. Test it in a synthetic twin."
categories: ["Data center", "Outages and failover"]
---

The design document says the room is N+1 for cooling. Six units are installed, five can carry the full design load, and any one of them can fail. It is a clear, sensible statement.

What it does not say is which unit, at what load, with which racks where, and with what else already out of service. Those details decide whether a failure is a non-event or the start of a long night.

## N+1 is a statement about totals

N+1 usually means the total cooling capacity with one unit missing is still enough for the total heat load. That is necessary. It is not always sufficient, because cooling is delivered to specific places. A unit at the end of the room mostly serves the racks near it. If it fails, the other units have to push air further, and the racks closest to the failed unit get the least of it.

So a room can have plenty of total capacity and still have a local hot spot when the wrong unit fails. Usually the worst case is the unit nearest the densest racks, which is also the unit working hardest day to day.

## How the margin erodes

When the room was designed, the load was spread evenly. Since then, a row of high-density racks has gone in at one end. A unit has been running with a degraded fan for months, waiting for a part. Another is scheduled for maintenance next week. None of these are failures, but each takes some of the margin the N+1 claim relied on.

The result is a room that is still N+1 in the spreadsheet, and closer to N in the corner where it matters.

## Failing each unit in a made-up hall

Consider an illustrative hall with six perimeter cooling units and four rows, the last of which holds dense compute. The synthetic twin holds the units, their capacity and condition, the racks and their heat load, and the room's airflow layout.

Failing each unit in turn gives six different answers. For four of them, inlet temperatures across the room rise a little and stay well within limits. For the unit at the far end, nearest the dense row, the twin shows the last three racks in that row climbing past their recommended inlet temperature. And if the unit with the degraded fan is treated as running at reduced output, failing its neighbor produces a similar result in a different corner.

Then the planning questions. If maintenance takes one unit offline next week, which other unit's failure during that window would cause trouble? The twin answers that directly, and it suggests doing the maintenance after the degraded fan is fixed, or temporarily shifting some load from the dense row.

## Checking your own N+1 claim

- Fail each cooling unit in turn, not just the total, and look at the racks nearest each one.
- Include units running below full output because of faults or pending repairs.
- Check what one more failure would do while a unit is down for maintenance.
- Watch where dense racks have been added since the room was designed.
- Keep containment and blanking in good order, since they decide how far the remaining units can push air.
- Revisit the claim whenever the load in a row changes significantly.

N+1 is a good design goal. Keeping it true takes a check against the room as it is today, one unit at a time.

Related reading: [why three racks run hot behind a containment gap]({{< ref "hot-aisle-containment-gap-three-hot-racks.md" >}}), [rehearsing maintenance and the second fault]({{< ref "rehearse-maintenance-second-fault.md" >}}) and [PDU phase imbalance]({{< ref "pdu-phase-imbalance-trips-rack-breaker.md" >}}). More in the [data center guide](/data-center/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
