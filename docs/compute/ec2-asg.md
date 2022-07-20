---
layout: default
title: EC2 Auto Scaling Group
parent: Compute
nav_order: 2
---

# EC2 Auto Scaling Group
Amazon Elastic Cloud Compute - Auto Scaling Group

- scale out (add) EC2 instances to match an increased load
- scale in (remove) EC2 instances to match decreased load
- ensure a minimum and maximum number of running EC2 instances
- super powers
  - automatically register new instances to an [ELB](../../networking-and-content-delivery/elb/)
  - automatically terminate and replace unhealthy instances

## Configuration
- Minimum Capacity
- Desired Capacity
- Maximum Capacity

## Attributes
- Launch Template
    - contains information on how to launch EC2 Instance
        - AMI + Instance Type
        - EC2 User Data
        - EBS Volume
        - Security Group
        - SSH Key Pair
        - IAM Role
        - Network + SUbnet Information
        - Load Balancer Information
- Min Size / Max Size / Initial Capacity
- Scaling Policy

## Auto Scaling
- optional configuration to scale an ASG based on CloudWatch Alarms
    - scale based on a selected Metric on Cloudwatch

## Launch Template
- versioning

## Health Checks
- automatically replace instances that fail health check
- can optionally enable ELB health check (if configured with ELB), in addition to EC2 health checks

## Scaling Policies 
### Dynamic Scaling
- Target Tracking Scaling
    - simplest to setup
    - set a target metric and scale in/out to keep the metric at that target
- Simple Scaling
    - setup own cloudwatch alarm triggers to trigger scale out / scale in rules
    - Scaling Action as triggered by a CloudWatch Alarm
- Step Scaling
    - Modified simple scaling
    - Define step: specify on rule how many units to add / remove at a time

### Scheduled Actions
- Anticipated scaling based on known usage pattern
- Useful when behavior is known in advanced
### Predictive Scaling
- continuously forcast load, and schedule scaling ahead
- New feature, machine-learning powered

## Metrics
- CPUUtilization - Average CPU
    - measures utilization aross your instances
- RequestCountPerTarget
- Average Network In/Out (if application is network-bound)
- basically, any metric that is the defined bottleneck where it is useful for the scaling events to react

## Scaling Cooldown
- Default is 300 seconds
- Time period after a scaling activity when ASG will not launch or terminate additional instance (to allow for metrics to stabilize)
