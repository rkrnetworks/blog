---
title: "A tale of two proposals: presales with and without a synthetic twin"
date: 2026-10-26T06:55:00Z
description: "RKR SETU 1.0 is now available in North America. Two vendors answer the same customer questions, one with slides and one with evidence from a synthetic twin of the building."
tags: ["presales", "network design", "RFP", "blast radius", "change management", "synthetic twin", "RKR SETU"]
slug: "presales-with-and-without-a-synthetic-twin"
audio: ["/audio/presales-with-and-without-a-synthetic-twin.mp3"]
audioDuration: "4:17"
cover:
  image: "/covers/presales-with-and-without-a-synthetic-twin.jpg"
  alt: "A tale of two proposals: presales with and without a synthetic twin (cover image)"
  hiddenInSingle: false
seoTitle: "Network presales proposals: with and without a synthetic twin"
seoDescription: "Two vendors answer the same customer questions: one with slides, one with evidence from a synthetic twin of the building. See which proposal holds up better."
categories: ["RKR SETU"]
---

RKR SETU 1.0 is now available in North America, alongside India, APAC and EMEA. To mark it, we made a short video about a part of the job that rarely gets attention: presales. Two vendors, one customer, and the same request.

## The request

The customer has a six-floor building. They want a change on floor three: contractor Wi-Fi, cameras powered over Ethernet, and three more access points. They want it live in six weeks. And they had two outages last quarter, which they'd like to understand before anyone touches the network again.

The questions that follow are the ones every presales engineer has heard. And the two outages last quarter? Show me floor three. What's the blast radius? Who signs off security? How will we know it worked?

## How it usually goes

Vendor A brings slides. About us, understanding your needs, a phased approach, assumptions, risks and next steps. It's a reasonable deck, and it's how most proposals look.

The trouble is what happens when the questions start. The answers stay on the slide. The outages are described rather than explained, floor three is a diagram, and most of the detail is still to be confirmed. None of that is anyone's fault. Without a model of the customer's network, there isn't much else a slide can say.

## The same meeting with a synthetic twin

The video below plays both meetings side by side on a made-up building.

{{< youtube NfPXaN5LKDU >}}

Watch it on YouTube: https://youtu.be/NfPXaN5LKDU

Vendor B answers the same questions in a synthetic twin of the building, using RKR SETU 1.0.

The two outages are reproduced, not described. In the video, eleven clients are affected. The design is checked rule by rule, and the change is committed in the model.

For security, the blocked path is shown hop by hop, with a retest attached. Floor three gets its three extra access points within the 490-watt power budget. The blast radius of the change is stated plainly: five access points and ten clients.

The change window is planned for a Friday night at 22:00, with the state committed, compared and ready to restore before cutover. To show that it worked, twenty flows are replayed. Then both designs go through the same checks, side by side.

The last part of the video is the one we think matters most. Without the twin, the assumptions stay assumptions, and they're marked as estimates. Question by question, one proposal defers and the other shows the evidence.

Same customer, same questions, a very different meeting.

## Why this matters before the deal, not after

Most of the risk in a network change is decided in presales. The design, the change window and the success criteria are often set before an engineer ever logs in. If those are built on estimates, the risk just moves to the night of the change.

Answering with evidence early changes the conversation. The customer sees their own floor, their own outages and their own blast radius. The vendor walks in prepared, and the design is tested before the customer has to test it in production.

## Practical takeaways

- Before a proposal, list the customer's questions and mark which ones you can answer with evidence and which with estimates.
- Reproduce past outages if you can. Customers remember them, and they shape how much a new design is trusted.
- State the blast radius in numbers: how many access points, how many clients.
- Agree on how success will be measured before the change, and test it the same way after.
- Put both designs, current and proposed, through the same checks.

If you haven't seen the product tour yet, start with [introducing RKR SETU 1.0]({{< ref "introducing-rkr-setu-synthetic-twin-network-it-ops.md" >}}).

Related reading: [what a synthetic twin of a network is]({{< ref "what-is-a-synthetic-twin-of-a-network.md" >}}) and [RKR SETU 1.0 in APAC and EMEA]({{< ref "rkr-setu-apac-emea-outdoor-access-point-install.md" >}}). More in the [RKR SETU overview](/setu/).

Demos are in person. Book a demo with our team: sales@rkr-networks.com
