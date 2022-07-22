---
layout: default
title: Route 53
parent: Networking and Content Delivery
nav_order: 3
---

# Route 53
Scalable domain name system (DNS)
- a reliable and cost-effective way to route end users to Internet applications
- highly available, scalable, and fully managed Authoritative DNS
- Also a Domain Name Registrar:
    - can register you own domain using Route 53
- With ability to check health of resources
- Only service with 100% SLA!
- Naming:
    - port 53 is the traditional DNS port

## DNS Info Dump
- Domain Name System
- Translates human-friendly hostname to the machine IP address
    - translate google.com -> 172.217.18.36

- Domain Registrar:
- DNS Records: A, AAAA, CNAME, NS
- Zone File:
- Name Server: resolves DNS queries (Authoritative or Non-Authoritative)
- Top Level Domain (TLD): .com, .us, .in
- Second Level Domain (SLD): amazon.com, google.com 
- Fully Qualified Domain (FQDN) Name:
    - http://api.www.example.com.
    - protocol://domain.subdomain.sld.tld.(root)

- How DNS Works
- recursively query DNS servers
    - 1: Local DNS
    - 2: Root DNS Server
    - 3: TLD DNS Server
    - 4: SLD DNS Server
    - then store info to local DNS, with TTL
![](../../../assets/images/how-dns-works.png)

## DNS Records
- A Record:
    - maps hostname to ipv4
- AAAA Record:
    - maps hostname to ipv6
- CNAME:
    - maps hostname to another hostname
    - target is a domain name with A or AAAA record
    - can't create a CNAME for the top node of a DNS namespace (Zone Apex)
    - e.g: cannot create CNAME for example.com. But can for www.example.com
- NS
    - Name servers for the hosted zone
    - IP / dnds names for servers that can respond to query for hosted zone
    - controls how traffic is routed to the domain
![](../../../assets/images/route-53-hosted-zones.png)

## Route 53 Hosted Zones
- Public Hosted Zone
    - contains records that specify how to route traffic to the internet (public traffic)
    - e.g. application.company  .com
- Private Hosted Zone
    - contains records that specify how to route your traffic within one or more VPCs (private domain names)
    - e.g. application.company.internal


## Route 53 TTL
- Time to Live
- High TTL (24 hours)
    - Less traffic to route 53 (DNS are cached longer)
    - Possibly outdated records
- Low TTL (e.g. 60 sec)
    - More traffic
    - But easy to change record
- Recommended values: 1 minute, to 2 days
- Mandatory, except for ALIAS record.

## Route 53 CNAME vs ALIAS
- Review: CNAME maps hostname to hostname.
- But not for root domain

- Alias: points Hostname to an AWS Resource
- Works for Root Domain and Non Root Domain
- Free of charge, with native healthcheck capability

## Route 53 Alias Records
- Maps hostname to AWS Resource
- Always of type A/AAAAA
- Can't set TTL manually
- Record Targets
    - ELB
    - Cloudfront Distributions
    - API Gateway
    - Elastic Beanstalk Environments
    - S3 Websites
    - VPC Interface Endpoints
    - Global Accelerator
    - Route 53 Record
  
## Routing Policies
- defines how Route 53 responds to DNS queries
- not actual traffic routing

### Simple
- typically, routing to a single resource
- if multiple values are returned, random one is chosen by client
- can't be associated with health checks

### Weighted
- Control the percentage of requests to go to a specific resource
- By assigning each record a relative weight
- DNS Records must have the same name and type
- Can be associated with health checks
- Assign a weight of 0 to stop sending traffic
- When all are 0, will be like simple routing

### Latency Based
- redirect to resource with leaest latency
- based on traffic between users and AWS Regions
- Can be associated with health checks

### Geolocation
- routing based on user location (different from latency based!)
- create default record in case no match on location
- location can be continent, or country

### Geoproximity
- use with Route 53 Traffic Flow (advanced feature)
- ability to shift more traffic to resources based on specified bias value
- for on-prem resources, can specify long and lat coordinates

### Multivalue
- use when routing to multiple resources
- can be associated with Health Checks
- used for Client-Side Load Balancing (not a substitute for ELB)
- Use over simple routing policy, to get option for health check

### Failover
- Use route 53 for active-passive failover for disaster recovery
- specify primary and secondary failover record type
- mandatory to specify health check on primary, optional on secondary

## Health Checks
-  only for public resource, normally
- Health check is primarily used for DNS Failover
- health check targets:
    - Monitor an endpoint
        - interval is 30 seconds by default or 10 seconds
        - can do text matching on the response for the first 5120 bytes
        - must allow incoming requests from route 53 health checkers!
    - Monitor other health checks (Calculated Health Checks)
        - aggregate health check other health checks
    - Monitor cloud watch Alarm (Full 
        control)
        - can be used to do health check on private hosted zones. 
        - create a cloudwatch metric for the private resource, then associate cloudwatch alarm to the route 53 health check

## Traffic Flow
- Visual editor to manage complex routing decision trees
- Configurations can be saved as Traffic Flow Policy
- helpful for geoproximity rule, with a visual representation of geoproximity rule bias value effect