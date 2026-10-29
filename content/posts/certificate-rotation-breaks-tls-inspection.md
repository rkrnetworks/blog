---
title: "A certificate rotation on the firewall broke one app: tracing TLS inspection failures"
date: 2026-10-29T10:00:00+05:30
description: "The firewall's inspection certificate was renewed on schedule. Browsers were fine, but one business application stopped connecting. A synthetic twin shows which clients and flows depend on that certificate before the next rotation."
tags: ["TLS inspection", "certificates", "firewall", "network security", "change management", "synthetic twin", "RKR SETU"]
slug: "certificate-rotation-breaks-tls-inspection"
audio: ["/audio/certificate-rotation-breaks-tls-inspection.mp3"]
audioDuration: "4:32"
cover:
  image: "/covers/certificate-rotation-breaks-tls-inspection.jpg"
  alt: "A certificate rotation on the firewall broke one app: tracing TLS inspection failures (cover image)"
  hiddenInSingle: false
---

Tuesday, 07:30. The security team renews the certificate the firewall uses to inspect encrypted traffic. It is a planned change, done a week before expiry. Browsers on managed laptops pick up the new certificate through the usual policy, and nobody notices anything.

Tuesday, 09:10. The warehouse team reports that their label printing application cannot reach its cloud service. The error says the connection is not trusted. By 10:00, the same is true for a finance tool on a handful of desktops and a set of sensors that upload readings every hour.

## What happened

When a firewall inspects encrypted traffic, it sits in the middle of the connection and presents its own certificate to the client. That only works if the client trusts the firewall's issuing certificate. Managed browsers usually do, because the trust is pushed by policy.

Many other clients do not use the operating system's trust store. Some applications bring their own list of trusted authorities. Some pin the certificate of their service and refuse anything else. Embedded devices often have a fixed store that was set up once, by hand, during installation. When the firewall's certificate changes, every one of those clients that had been quietly trusting the old one, or had been exempted by a rule tied to the old one, can fail at once.

In this case, three things were true. The label printing application had been given a manual trust entry for the old issuing certificate years ago. The finance tool had been on an inspection bypass list kept in the decryption profile tied to the old certificate, and the rotation replaced that profile along with the certificate. And the sensors had the old certificate loaded into their own configuration.

## Why nobody saw it coming

The certificate renewal was a security task. The applications belonged to three different teams. The bypass list lived on the firewall, the manual trust entries lived on individual machines, and the sensors were managed by facilities. There was no single place that said "these flows depend on this certificate."

The change ticket asked the right question, "what uses this certificate?", but the only available answer was "the firewall."

## Laying out the dependencies

In an illustrative company network, the synthetic twin holds the firewall's inspection policy, its bypass rules, and the client groups and applications whose traffic crosses it. It also holds which of those clients rely on system trust, which carry their own, and which are exempt.

Swapping the inspection certificate in the twin produces a list of affected flows instead of a surprise. Managed browsers carry on. The label printing hosts fail, because their trust is manual. The finance tool falls out of its bypass and starts failing inspection. The sensors fail outright.

That list turns into a plan. Update the manual trust on the label printing hosts before the rotation. Rewrite the bypass rule so it does not depend on certificate details. Schedule the sensor update with facilities. Then run the rotation again in the twin and confirm nothing else changes.

## Before the next rotation

- Keep a list of clients that do not use system trust, including applications and embedded devices.
- Make inspection bypass rules depend on destinations or categories, not on certificate details that will change.
- Ask every team that owns devices behind the firewall whether anything was trusted by hand.
- Rotate well ahead of expiry, so there is room to fix what breaks without an emergency.
- Test with real client types, not only a browser.
- After the rotation, check the firewall's handshake failures by application for a day or two.

Certificate rotation is routine, and it should be. The trouble is that the old certificate may have been propping up more than anyone wrote down.

Demos are in person. Book a demo with our team: sales@rkr-networks.com
