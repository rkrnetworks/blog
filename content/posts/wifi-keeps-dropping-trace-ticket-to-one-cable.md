---
title: "Wi-Fi keeps dropping on one floor: tracing the ticket to one cable"
date: 2026-10-28
description: "One AP goes silent and a floor's Wi-Fi keeps dropping. How teams usually chase it, and how a synthetic twin takes the ticket to one cable in a closet."
tags: ["Wi-Fi troubleshooting", "access point", "PoE", "root cause analysis", "MTTR", "synthetic twin"]
slug: "wifi-keeps-dropping-trace-ticket-to-one-cable"
cover:
  image: "/covers/wifi-keeps-dropping-trace-ticket-to-one-cable.jpg"
  alt: "Wi-Fi keeps dropping on one floor: tracing the ticket to one cable (cover image)"
  hiddenInSingle: false
audio: ["/audio/wifi-keeps-dropping-trace-ticket-to-one-cable.mp3"]
---

It's 21:40 and a ticket comes in. Guests on floor 8 say the Wi-Fi keeps dropping. It's not a full outage, just people walking from one end of the floor to the other and losing their connection. Nobody has said which corner, and nobody has said which access point, because guests don't know what an access point is.

This is one of the most common tickets a network team gets, and one of the most tedious to chase.

## How this usually goes

The standard path goes something like this. Log into the wireless controller and look for an AP on floor 8 that isn't happy. If one isn't joined, the familiar "access point not joining controller" checklist starts: is it getting power, does it have an address, is the switch port up, is PoE enabled, is it the cable?

To answer those, you leave the controller and log into the switch CLI to find which port the AP is on. Then you check the PoE table. Then you check the cable records, if there are any, to see which run goes where. If the records are thin, someone walks to the closet with a tester and starts tracing.

Every step is a different tool and often a different person. The wireless team owns the controller, the network team owns the switches, and someone on site does the walking. Even when everyone is quick, there are handoffs. And it's common to make more than one trip to the closet before anyone touches the actual fault, because the first trip was to look and the second is to fix.

None of this is hard. It's just slow, and it happens at 21:40 while guests are on a bad connection.

## Start at the answer instead of the first login

The demo below works the same ticket on a synthetic twin of a made-up building, from one CLI session. The fault, a cut on Cable 137, was introduced before the take.

{{< youtube 4riaNkTYD-Y >}}

It opens with floor 8. There are 7 access points on the floor and 6 of them are on air, with 18 client devices connected.

One question finds the quiet one. Out of 85 radios in the building, one is silent: F8-AP-07. It isn't beaconing, and it isn't joined to its controller.

Then comes the chain. Following F8-AP-07 down the building shaft to its closet shows that switch R8-SW01 powers it and carries its uplink, which is Cable 137. That cable is down, with no power reaching the AP. Meanwhile, 8 guest devices have already roamed to neighbouring access points, which fits a ticket that says "keeps dropping" rather than "no Wi-Fi".

The power check agrees. PoE on that port is on and searching, and nothing answers on Cable 137. That rules out a PoE setting. The root cause is written down as the cable run or the AP itself.

That leads to the instruction for the tech, which is specific: test Cable 137 first, from R8-SW01 to F8-AP-07, and the AP second. There's no guessing which closet.

Finally, the fix is simulated on the twin. Cable 137 is restored, the link comes back, and there are no silent radios left. Every access point is beaconing again.

In this take it was 63 seconds from ticket to root cause, typing included. One cable was found, along with the closet, switch and AP it feeds, and zero devices were logged into to find it. Your own times will depend on the fault and the site, but the method stays the same.

## What changes for the team

The biggest change is where the engineer starts. Instead of opening the first console and working inward, they start with the answer: this AP, this switch, this cable. The remaining work is confirming and fixing it.

That has knock-on effects that matter more than the 63 seconds. Fewer people are pulled into each incident, because nobody has to hop between the controller, the switch and the PoE tables. There are fewer truck rolls, because the tech who goes to the closet knows which cable to test and what to bring. And guests spend less time on a bad connection.

It also gives a better ticket record. "Cable 137 between R8-SW01 and F8-AP-07, cable or AP, not PoE" is a much more useful line in the ticket history than "rebooted AP, seems fine now."

SETU works alongside the Cisco, Aruba, Juniper and Arista gear you already run. RKR doesn't sell hardware.

## Practical takeaways

- When a floor's Wi-Fi "keeps dropping" rather than going down entirely, suspect one silent AP with neighbours picking up its clients. Look for the radio that isn't beaconing before tuning anything.
- Treat "not joined to the controller" plus "PoE on and searching" as a strong hint toward the cable run or the AP, not the switch config.
- Keep AP-to-port-to-cable records somewhere you can query at 21:40, not just in a spreadsheet on someone's laptop.
- Give the tech one specific instruction: which cable, from which switch to which AP, and what to test second. It saves the second trip.
- Write the root cause into the ticket in those terms. Next time the same AP goes quiet, the history will help.
- Faults at night are when your process gets tested, whether the cause is a cut cable or someone poking at your network. Attackers practice. Your engineers should too.

For the bigger picture of how this works, see [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}). For a louder version of the same idea, the [UPS on battery post]({{< ref "ups-on-battery-what-goes-dark.md" >}}) traces six alarms to one root cause.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
