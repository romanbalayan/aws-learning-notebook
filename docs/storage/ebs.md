---
layout: default
title: EBS
parent: Storage
nav_order: 1
---

# EBS Volume
Amazon Elastic Block Store (EBS) Volume
- Block Storage Volumes for [EC2 Instances](../../compute/ec2)
- Network drive (not a physical drive) that can be attached to instances, which allows data to be persisted even after instance termination

## Info Dump
- Locked into an availability zone
    - how to move volume accross AZs?
    -
- Can only be attached to a single volume (generallyy)
- Provision capacity:
    - size (GB)
    - IOPS (input/output operations per second)
- Delete on Terminate Attribute
    - On the ec2 creation wizard, when attaching EBS volume, there is an attribute to specify behavior of EBS upon instance termination.
    - by default, initial attached volume (root volume) has attribute checked.
    - not checked for new additional volumes (volume is preserved when instance is terminated)
- Block storage - still need to format EBS volume after attaching. (out of scope for now)

## EBS Snapshot
- backup (snapshot) of EBS Volume state at a point in time
- CAN run creation of snapshot even when volume is attached. But, recommended to detach
- Use case: For backup
- Other use case: To copy to another instance in a different AZ or region
- Where are EBS Snapshots stored
- How are EBS Snapshot stored (if a snapshot daily, for example)

- EBS Snapshot Archive
  - Move snapshot to "Archive" Tier (setting in S3?)
  - 75% cheaper, but takes 24 to 72 hours for restoring the archive
- Recycle Bin for EBS Snapshot
  - setup rule to retain deleted snapshot (save accidental deletion)
  - specify retention period - 1 day to 1 year 

## EBS Volume Types
- 6 types (as of nn)
- More info for AWS Solutions Archi?

| Volume Type         | Description               | Some Use Cases                 |
| :----------------   | :------------------------ | :----------------------------- |
| gp2/gp3 (SSD)       | General Purpose SSD       | Balanced Price and Performance |
| io1/io2 (SSD)       | Highest performance SSD   | Mission critical, high performance workloads |
| st1 (HDD)           | Low Cost HDD Volume       | Frequently accessed, high throughput |
| sc1 (SSD)           | Lowest Cost SSD Volume    | Infrequently accessed |

- Consult docs for Size | Throughput | IOPS limits
- only gp2/gp3 and io1/io2 can be used as boot volume

### GP3
- 1GiB to 16 TiB
- Baseline 3000 IOPS
- Baseline 125 MiB/s
- Can increase IOPS up to 16000 
- Throughput up to 1000MiB/s 
- Independently!

### GP2
- 1GiB to 16 TiB
- Burstable until 3000 IOPS, for small volumes?
- Throughput is also linked to IOPS
- IOPS performance is linked to size of volume, max at 16000 IOPS
- 3 IOPS / GB: Max IOPS at 5334 GB

### Provisioned IOPS SSD 
- Use case for applications with sustained IOPS performance
- Or applications that need more than 16000 IOPS
- Typical use case for database workload (that requires high, consistent throughput)
- io2/io1
  - Max PIOPS = 64000 (for nitro instances)
  - Max PIOPS = 32000 for other
  - Can increase IOPS independently from Size
  - Storage size is 4GiB to 16TiB

### io2 Block Express
- 4 GIB to 64 TiB Storage size
- 256000 Max PIOPS
- !! Supports EBS Multi-Attach


### Hard Disk Drives HDD 
- Cannot be boot volume
- 125 Mib to 16TiB

- Throughput optimized: st1
  - max throughput 500 MiB/s and 500 IOPS
  - processing large log files, data warehousing 
- Cold HDD: sc1
  - For frequently accessed data
  - When cost is top importance
  - Max throughput: 250 MiB/s and 250 IOPS