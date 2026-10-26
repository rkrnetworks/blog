---
title: "Wi-Fi connected, no IP address: tracing DHCP into the data hall"
date: 2026-10-26T07:00:00Z
description: "Two new wireless clients can't get an address, while every port is up. A synthetic twin follows the request from the office into the data hall and finds one host sending the reply down the wrong cable."
tags: ["DHCP", "Wi-Fi troubleshooting", "virtualisation", "data center", "root cause analysis", "synthetic twin", "RKR SETU"]
slug: "wifi-connected-no-ip-address-dhcp-data-hall"
audio: ["/audio/wifi-connected-no-ip-address-dhcp-data-hall.mp3"]
audioDuration: "4:03"
cover:
  image: "/covers/wifi-connected-no-ip-address-dhcp-data-hall.jpg"
  alt: "Wi-Fi connected, no IP address: tracing DHCP into the data hall (cover image)"
  hiddenInSingle: false
---

A wireless client joins the network and gets no IP address. Then another. Two new clients can't work, while two others on the same floor are fine. Three sites, 113 access points, and every port is up.

This is one of those tickets that bounces between teams. The wireless team sees a client that associated. The switch team sees ports that are up. The data center team sees servers that are running. Each of them is right, and the client still has no address.

## Why this one hides

An address request travels a long way. It goes from the client through the access point, the switch and the relay, and on into the data hall where the service runs. The reply has to make the same journey back. Most troubleshooting looks at one hop at a time, and every single hop here looks healthy.

The cause in this case isn't a failure at all. It's a decision, made by a host in the data hall, about which cable to send the reply on.

## Following the request in a synthetic twin

The video below follows the request on a synthetic twin of a made-up three-site network.

{{< youtube -_aNHX4vysw >}}

Watch it on YouTube: https://youtu.be/-_aNHX4vysw

In the data hall, a host picks which cable each reply leaves on. Before the change, the service answers on the service cable, and everything works.

Then a live migration. A running server moves to a new host and keeps its address. It's routine work: every port up, nothing down.

The client asks for an address, through the access point, the switch and the relay. The request reaches the service, now on its new host, and it answers with an offer. But the reply goes out on uplink one. The host picks that cable by a hash of the sender's port, and on this host, uplink one is the storage cable. So the reply lands on the storage network, and the storage port drops it. Correctly.

The cause is a naming mismatch. Both hosts call it uplink one, but the cables differ. On the new host, uplink one leads to the storage port.

The twin also answers the next question, which is who else is affected. Every new lease, and every uncached name the service answers. As a control, a port group that nothing here uses is changed, to show it isn't the cause.

The repair is to map the new host's cables the same way as the old one. The request goes through again, and the wireless client has its address.

The links never went down. A decision did.

## What to take from it

A move that keeps every port up can still change the path a reply takes. In virtualised data centers, where workloads move between hosts as a matter of routine, "same name" doesn't always mean "same cable". The difference only shows up when you follow a real request end to end, through the wireless side, the campus and the data hall together.

That's the reason we keep campus and data center in one synthetic twin, rather than as separate pictures. It's the same story in our post on [tracing a Wi-Fi ticket to one cable]({{< ref "wifi-keeps-dropping-trace-ticket-to-one-cable.md" >}}), from the other end of the network.

## Practical takeaways

- When some new clients fail and others work, look at what changed for the new ones, including where their requests are now answered.
- Follow the reply, not just the request. A reply that leaves on the wrong cable looks like silence to the client.
- Check that hosts in the same cluster map their uplinks to the same physical cables, not only the same names.
- After a live migration, test a fresh lease, not only an existing session.
- Use a control change to rule things out, so the fix you make is the one that matters.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
