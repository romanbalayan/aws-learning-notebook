---
layout: default
title: EC2
parent: Compute
nav_order: 1
---

# EC2
Amazon Elastic Cloud Compute
- Virtual servers in the cloud
- Secure and resizable compute capacity for virtually any workload

## Configuration
- Operating System: Linux, Windows, or MacOS
  - Amazon Machine Image (AMIs)
- Instance Type (more info for AWS Solutions Architect)
- Compute power and Cores (CPU)
- Memory (RAM)
- Storage Space
  - Network Store (EBS and EFS)
  - Hardware (EC2 Instance Store)
- Network (IP Address)
- Firewall: Security Group
- Bootstrap Script

## EC2 User Data
- Script ran at first instance boot (only ran once, on first launch)
- Script is executed as root user (no need for sudo)

## Instance Types
- Reference: [http://aws.com/ec2/instance-types](http://aws.com/ec2/instance-types)
- Naming Convention: m5.2xlarge
- m: instance class
- 5: generation
- 2xlarge: size of the instance class

| Instance Type         | Instance Class (some) | Short Description                                                                                                                      |
| :-------------------- | :-------------------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| General Purpose       | T2, T3, M4, M5        | Balanced compute, memory, and network                                                                                                  |
| Compute Optimized     | C4,C5                 | High perfomance processor, heavy on compute                                                                                            |
| Memory Optimized      | R4, R5, X1            | Memory as in RAM. For processing large data sets in memory                                                                             |
| Storage Optimized     | H1, D2, D3, I3       | Processes needing high sequential read and write to local storage (Disk)                                                               |
| Accelerated Computing | P2, P3, P4, G3, G5    | Instances using hardware accelerators (GPU), or co-processors (floating point calculation, graphics processing, data pattern matching) |

- Naming Convention: m5.2xlarge
- m: instance class
- 5: generation
- 2xlarge: size of the instance class
- Match expected workload to a suiting instance type

## Provisioning Options
1. On Demand Instance - Bill by the second. Pay for what you use (for linux and windows). For other OS, pay by the hour
1. Reserved Instance - reserve for 1 or 3 years
  - Reserved Instance - Fixed Instance Type
  - Convertible Reserved Instance - Fixed time, but can change instance type
  - Locked region, instance type, OS, and tenancy
1. Spot Instance - Cheapest Option - but unreliable - can lose instance when instance price goes above bid price

Tenancy
1. Dedicated Instance - reserve an instance hardware. Ensures hardware is not shared with other users. On restart, may change to a different hardware, but with the same assurance that instance is not shared.
1. Dedicated Host - reserve an entire physical server - when control of instance placement is required
1. Capacity Reservation??


## AMI
- Amazon Machine Image
- Customization of EC2 Instance 
  - include os, software configuration, monitoring, etc
  - faster boot time (for example, vs placing all the configuration from EC2 User Data)
- Sources
  - Public AMI: AWS Provided
  - Own AMI: Self made and maintained
  - AMI Marketplace: pre-made (or sold) by other parties

- Own AMI
  - Can create an image from an existing EC2 instance

## EC2 Instance Store
- High-performance hardware disk (vs EBS network drive)
- Physical hardware disk attached to Ec2 Instance
  - if network latency is not acceptable
- But, storage is ephemeral. Data is lost if instance is **stopped** (not just terminated!)
- Meaning, not for long term storage
- Instance types with instance store are i3 instances (Storage optimized) 

## Info Dump
- Instance metadata: 169.254.169.254/latest/meta-data/
- can get IAM Role Name (and ARN?), but not the Policy
  - endpoint to get instance data, without the need for IAM Role
    - Instance metadata: 169.254.169.254/latest/meta-data/iam/security-credentials/_RoleName_
    - Returns short lived credentials: AWS Access Key Secret Key, Token
  - host info, network info, etc
- Instance User Data: 169.254.169.254/latest/user-data
- EC2 Instance Connect - web-browser based ssh connection to EC2 Instance on AWS Console. But only works with Amazon Linux 2 Image

## Gatchas
- By default, EBS volume attached on an EC2 instance is deleted on termination