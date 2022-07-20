---
layout: default
title: EFS
parent: Storage
nav_order: 2
---

# EFS
Amazon Elastic File System
- Fully managed File System for [EC2 Instances](../../compute/ec2)

## Configuration
- Performance mode
  - General Purpose
  - Max I/O
  
- Throughput mode
  - Bursting - throughput scales as file system grows
  - Provisioned - specify throughput independent of amount of data stored
    - 1 to 1024 MiB

- Storage Classes
  - Standard Storage Class - available for Multiple AZs
    - EFS Standard
    - EFS Standard-Infrequent Access (EFS-IA) - Lower price to store, extra charge to retrieve
  - One Zone Storage Class
    - EFS One Zone
    - EFS One Zone-Infrequent Access
  - Can control storage tier with a lifecycle management policy

## Info Dump
- Managed Network File System - can be mounted on multiple EC2 instances
- Can work on EC2 instances in different AZs
- Highly available, scalable, and expensive ~3x of GP2

- Uses NFSv4.1 (and NFSv4.0) protocol
- Access is controlled by security groups
- Only compatible with linux AMI
  - uses POSIX file system
- Automatically scales. Pay for what you use
- Multiple (thousands) of compute instances can access at the same time
  - including EC2, EC2, and AWS Lambda