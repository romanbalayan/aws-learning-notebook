---
layout: default
title: GLB
parent: ELB
grand_parent: Networking and Content Delivery
nav_order: 4
---

# Gateway Load Balancer 
- Deploy, scale, and manage fleet of 3rd party network virtual appliances in AWS
- For network traffic inspection
- Operates on Layer 3 (Network Layer)
- sample use cases:
    - Firewall
    - Intrusion Detection and Prevention Systems
    - Packet Inspection systems
    - Payload Manipulation
- Transparent to destination application
- GENEVE protocol on port 6081 
- Desinations are Target Groups (same as ALB, and NLB)
