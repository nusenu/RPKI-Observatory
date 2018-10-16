---
title: RPKI Unreachable Networks
keywords: RPKI, BGP, routing, security, Internet
sidebar: unreachable_sidebar
permalink: unreachable-networks.html
---

## What is a RPKI unreachable network?

A "RPKI unreachable network" is IP space that
* is announced via a BGP prefix-origin pair that has a [RPKI](https://en.wikipedia.org/wiki/Resource_Public_Key_Infrastructure)
validity state of "INVALID" 

**and**
* is not covered by any other **usable** announcement (via "VALID" or "UNKNOWN"
less-specifics or multiple "VALID" more-specifics that cover the same IP address space).

In the context of this website you will see the short form "unreachable network(s)" - without 'RPKI' and also
"Unreachable IP space" or "unreachable prefixes".

These networks are unreachable by networks that perform RPKI-based Route Origin Validation (ROV).
Either because they perform ROV themselfes or because all the IXPs they connect to
perform ROV for them on the Route Servers (and have no other BGP sessions).
To be precise: An "RPKI unreachable network" can sent packets **to** ROV-enabled
networks but it will not receive any packets in reply (due to the lack of a return path/route).

This issue is in most cases caused by a RPKI Route Origin Authorization (ROA) misconfiguration (ASN or max length mismatch).

## Is any of my prefixes affected?

This page was specifically created to help you answer this question.
You can search the affected networks by 
* Autonomous System Number (ASN)
* Autonomous System Name and 
* specific prefixes 

to find out if your network's reachability suffers from this kind of RPKI misconfigurations.

## Why should I care if my network is listed as unreachable?

We assume every network operator wants their BGP announcements to be visible 
and reachable (unless they are special test prefixes that are unreachable on
purpose to test ROV).

## What am I supposed to do if one of my prefixes is listed as unreachable?

The prefixes are unreachable because their BGP announcements 
do not match the Route Origin Authorization (ROA). If you are the
IP holder you can update the ROA to match your announcement and your prefix
will become reachable again.

If your customer is the IP holder of the prefix (and you are just announcing
the prefix for your customer) your customer is responsible for updating the ROA.

## Where can I update the causing ROA to make my IP space reachable again?

That depends from which RIR you got the IP space from:
* [APNIC](https://apnic.net/roa) ([video](https://www.youtube.com/watch?v=hzCVvnjo6V8))
* [LACNIC](https://lacnic.zendesk.com/hc/en-us/sections/206490008-RPKI) ([video](http://www.lacnic.net/2832/1/lacnic/))
* [RIPE NCC](https://www.ripe.net/manage-ips-and-asns/resource-management/certification/resource-certification-roa-management) ([video](https://www.youtube.com/watch?v=gLwHp12wOGw))
* [ARIN](https://www.arin.net/resources/rpki/using_rpki.html)
* [AfriNIC](https://www.afrinic.net/en/initiatives/resource-certification)

## Can you notify me next time you spot this problem on one of my networks?

We do not aim for such a service but we encourage every network operator to use
already available services for that. If you are in the RIPE region you can use
the notification service in RIPE's RPKI dashboard ([video](https://www.youtube.com/watch?v=gLwHp12wOGw)).
For IP space outside the RIPE region other monitoring and alerting services like BGPmon are available.


## How do you find unreachable IP space?

We use a local [RPKI validator 3](https://github.com/RIPE-NCC/rpki-validator-3/wiki) instance as our data source,
which itself uses RIPE's [RIS](https://www.ripe.net/analyse/internet-measurements/routing-information-service-ris) data.

For some more background information see this [blog post](https://blog.apnic.net/2018/10/16/cleaning-up-roas-inconsistent-with-the-bgp-state/).

## How do you map ASNs to countries?

[RIPEstat](https://stat.ripe.net) is used to map ASNs to country codes and to get
AS names.

## How can I verify the data on this page?

You can verify every listed prefix by clicking the "reason" field (at the prefix level).
That URL will bring you to RIPE's public [RPKI Validator instance](https://rpki-validator.ripe.net).

## What does the "affected" column mean?

A given prefix can be affected:
* complete(ly): means the entire prefix is RPKI-unreachable

or

* partial(ly): means some parts of the prefix are RPKI-unreachable (see Figure 5 on this [page](https://blog.apnic.net/2018/10/16/cleaning-up-roas-inconsistent-with-the-bgp-state/).
for an example).

## What is the "reason" column for?

The "reason" column should provide an indicator as to why a given announcement has the RPKI validity state "INVALID" (good to know when trying to solve it).

There are two possibilities why a given prefix-origin pair might be in an "INVALID" state:

Either it is announced by an unauthorized ASN (reason: "INVALID ASN") or
it is announced via a more-specific prefix that is not authorized due to the [max length](https://www.youtube.com/watch?v=I3Owb0u8Wuk) value.

## How often are the lists of unreachable networks updated?

Pages are usually generated between daily and weekly. Every page 
shows a timestamp at the top.

## I found a false-positive / false-negative!

Before reporting FP/FN please be aware that the data on this page
isn't real time data. So if you made an affected prefix reachable again by updating the ROA
or BGP announcement it will not be immediately disappear from this page (but it should within a week or so).

That said if you found one that persists on this page for more than a week
it would be great if you could report it using the feedback email address (button on the top).
Please make sure to include the timestamp data that is shown on the page when reporting issues.
