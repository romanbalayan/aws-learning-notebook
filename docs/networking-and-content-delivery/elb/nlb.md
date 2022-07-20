---
layout: default
title: NLB
parent: ELB
grand_parent: Networking and Content Delivery
nav_order: 3
---

# Network Load Balancer 
- v2 AWS Load Balancer
- Layer 4
    - Forward TCP or UDP traffic
    - handle millions of request/second
    - less latency (vs ALB) ~100ms vs ~400ms
- one static IP per AZ, with support for assigning elastic ip
    - important use case for IP Whitelisting
- Target Groups
    - EC2 Instances
    - IP Address - private IPs only (on-prem target use case)
    - ALB (to combine IP whitelisting NLB fixed IP with ALB use case)

- NLB Info Dump
    - Application server will see IP of the client directly (side effect of level 4 load balancing?)
    - NLB are not assigned with a security group!
    - connection is sticky by default?
