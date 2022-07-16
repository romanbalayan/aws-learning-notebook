---
layout: default
title: VPC
parent: Fundamentals
nav_order: 2
---

# VPC

- Amazon Virtual Private Cloud
- Logically isolated virtual network inside of AWS Cloud

## Components
- VPC
- Subnet
- Internet Gateway
- NAT Gateway


## Security Group
- Control how traffic is allowed in or out of EC2 Instances
- Firewall on instance level
- Only contain **allow** rules, and can reference either IP address or other Security Groups
- If application is not accessible (timeout) - usually a sec group error! (vs connection refused)
- by default: All inbound traffic are denied (implicitly, no inbound rules). All outbound traffic are allowed (explicitly, 0.0.0.0/0 is allowed on all ports)