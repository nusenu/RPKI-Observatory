---
title: "The RPKI Observatory"
sidebar: home_sidebar
permalink: index.html
accordion: false
---

## What is the RPKI Observatory? 

The RPKI Observatory analyzes multiple aspects of the deployed
[Resource Public Key Infrastructure](https://en.wikipedia.org/wiki/Resource_Public_Key_Infrastructure) (RPKI)
landscape.

## What are the goals of the RPKI Observatory?

* measure how widespread common RPKI configuration issues actually are
* rise awareness for them
* provide actionable information for RPKI adopters to solve common issues
* increase the RPKI adoption and ROA IP space coverage
* gather RPKI and routing security metrics
* analyze trends in RPKI deployments
* encourage the deployment of route origin validation (ROV)

* **overall goal**: increase Internet routing security against BGP hijacking attacks and unintended misconfigurations

## Non-Goals

We do not aim to be a RPKI issue notification service for individual network operators
since there are already solutions for that (RIPE NCC's RPKI dashboard for RIPE IP space
and BGPmon).

## How does it work?

Every module works mostly independently.
Our first module ("RPKI Unreachable Networks") consumes data
from a local [RPKI validator](https://github.com/RIPE-NCC/rpki-validator-3/wiki) 
instance which itself pulls in data from [RIPE RIS](https://www.ripe.net/analyse/internet-measurements/routing-information-service-ris).
To be able to display AS names and country codes we query [RIPEstat](https://stat.ripe.net).

## Who is the target audience?

* BGP Network Operators
* NOG Communities
* IXPs
* Regional Internet Registries (RIRs)
* everyone interested in RPKI, Internet Routing Security and Internet metrics and measurements.
