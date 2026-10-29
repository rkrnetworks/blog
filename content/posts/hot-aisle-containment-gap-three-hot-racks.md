---
title: "A gap in hot aisle containment: why three racks run hot and the rest don't"
date: 2026-10-29T10:00:00+05:30
description: "Three racks at the end of a row run warmer than the others, even though cooling capacity is fine. A synthetic twin of a made-up data hall traces it to a gap in containment and shows what closing it changes."
tags: ["data center", "hot aisle containment", "airflow", "cooling", "capacity planning", "synthetic twin", "RKR SETU"]
slug: "hot-aisle-containment-gap-three-hot-racks"
audio: ["/audio/hot-aisle-containment-gap-three-hot-racks.mp3"]
audioDuration: "3:42"
cover:
  image: "/covers/hot-aisle-containment-gap-three-hot-racks.jpg"
  alt: "A gap in hot aisle containment: why three racks run hot and the rest don't (cover image)"
  hiddenInSingle: false
seoTitle: "Hot aisle containment gap: why three racks run hot"
seoDescription: "Three racks at the end of a row run hot while cooling capacity looks fine. Trace it to a gap in hot aisle containment, and what closing it changes, in a twin."
categories: ["Data center"]
---

The row has twelve racks. Nine of them have inlet temperatures where you would expect. The last three, at the end nearest the wall, run several degrees warmer. The cooling units have spare capacity, the setpoints are fine, and the racks are not unusually dense.

When the facilities team finally walks the row with a handheld sensor, they find it. The end door of the hot aisle containment does not seal, and there is a gap above the last rack where a cable tray passes through. Hot exhaust air is leaking back into the cold side and being drawn straight into the nearest servers.

## Why a small gap matters so much

Containment works by keeping hot and cold air apart. Cooling units supply cold air into the cold aisle, servers pull it through, and the hot exhaust goes back to the coolers without mixing. When that separation holds, the inlet temperature is close to the supply temperature everywhere along the row.

A gap breaks that. The pressure difference across containment pushes hot air through any opening, and the racks nearest the opening breathe it in. The cooling units cannot fix this by working harder, because the problem is not too little cold air. It is warm air in the wrong place.

The effect is local, which makes it easy to misread. Three hot racks next to nine normal ones look like a rack problem, maybe a dense server or a failing fan. Teams often respond by lowering the setpoint for the whole room, which costs energy everywhere to fix a gap in one place.

## What the twin adds

Take an illustrative data hall with four rows of contained hot aisles. The synthetic twin holds the racks, their load, the cooling units and the containment itself, including doors, panels and the places where trays pass through.

With the end door modeled as leaking, the twin shows the same pattern the facilities team found: the last three racks warming, the others steady. With the door sealed and a brush strip added where the tray passes through, those three racks come back in line with the rest of the row.

The twin can also answer the question that usually comes next. If the plan is to add two more racks to that row next quarter, where should they go? With the gap fixed, the end positions are fine. With the gap still open, those would be the worst positions in the row.

The point is not to replace the walk with the twin. It is to let the team ask what a fix would do, and what a planned change would do, before moving any hardware.

## A short containment check

- Walk each contained aisle and check end doors, roof panels and the seals where cable trays and pipes pass through.
- Fit blanking panels in every empty rack unit, including at the top and bottom of racks.
- Compare inlet temperatures along each row. A gradient toward one end usually points to a leak at that end.
- Fix the leak before lowering the room setpoint.
- Before adding racks to a row, check where the containment is weakest and avoid putting new load there until it is fixed.
- Re-check after any work that opens containment, such as cable pulls or tray changes.

Containment problems are rarely complicated. They are just easy to miss when the symptom shows up at the rack and the cause is in a seal three meters away.

Related reading: [whether the room is really N+1]({{< ref "crac-unit-fails-is-the-room-really-n-plus-one.md" >}}), [cable tray fill for a new row]({{< ref "cable-tray-fill-before-adding-a-row.md" >}}) and [PDU phase imbalance]({{< ref "pdu-phase-imbalance-trips-rack-breaker.md" >}}). More in the [data center guide](/data-center/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
