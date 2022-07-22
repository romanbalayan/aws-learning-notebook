---
layout: default
title: ALB
parent: ELB
grand_parent: Networking and Content Delivery
nav_order: 2
---

# Application Load Balancer 
- v2 AWS Load Balancer
- Layer 7 (HTTP)
- Allows:
    - load balancing to multiple http applications across machines (target groups)
    - load balancing to multiple applications on the same machine (e.g. containers)
    - support for http/2 and web socket
    - support http to https redirect

- Routing tables to different target groups
    - routing based on path in url
        - example.com/users and example.com/posts
        - will be routed to diff target groups
    - routing based on hostname in url
        - one.example.com and other.example.com
    - routing based on query string, headers
        - example.com/users?id=123&order=false
- Great fit for Docker and Amazon ECS
    - port mapping feature?

- Target Groups
    - EC2 Instances (can be managed by an Auto Scaling Groups)
    - ECS Tasks
    - Lambda Functions
    - IP Addresses (private IPs only!)

- a single ALB can route to multiple target groups
- health checks are done at the target group level

## ALB Info Dump
- Fixed hostname `<alb-name>-<internal_id>.region.elb.amazonaws.com`
- Application server will not see IP of the client directly
    - true client ip is in header: X-Forwarded-For
    - port: X-Forwarded-Port, protocol: X-Forwarded-Proto
    - this is due to connection termination at ALB level
- access control using security groups

- Authenticate Users using ALB
  - can be configured to securely authenticate users, to offload from application.
  - support authentication using User Pools supported by Amazon Cognito