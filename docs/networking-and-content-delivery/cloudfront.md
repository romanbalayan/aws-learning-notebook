---
layout: default
title: Cloudfront
parent: Networking and Content Delivery
nav_order: 4
---

# AWS Cloudfront
Securely deliver content with low latency and high transfer speeds
- Content Delivery Network (CDN) 
- 410+ Points of Presence (400+ Edge locations and 13 regional mid-tier caches) 
- Great fit for use for static content that must be available everywhere (that can be outdated)

## CloudFront - Origins
- S3 Bucket
    - For distributing files and caching at the end
    - enhanced security with OAI (Origin Access Identity)
    - Can be used as ingress, to upload files to s3
- Custom Origin (HTTP Endpoint)
    - Application Load Balancer
    - EC2 Instance
    - S3 Bucket (enable bucket as static S3 Website)
    - Any HTTP Bucket (can be on-premise)

## Origin Access Identity
- OAI
- IAM Role for Cloudfront Origin
- Restricts S3 Bucket Access to Cloudfront
- Security layer for Cloudfront + S3 Bucket Policy

## ALB or EC2 as Origin
- Ec2 Instance must be Public (if direct to EC2)
- will traverse EC2 Security group - must have security group to allow ALL CDN endpoints (provided by AWS)

- For ALB - ALB must be Public, then underlying EC2 may be private
- same Sec Group allow rule for ALB to llow CDN Endpoints

## Geo Restriction
- Restriction of access by location
    - Whitelist
    - Blacklist
- Country is determined by 3rd Party Geo-IP Database


## CloudFront Caching
- Cache based on multiple parameters:
    - Headers
    - Session Cookies
    - Querystring Params
- Minimize request to origin, by maximizing cache hit rate
- Control TTL (0 seconds to 1 year)
- Can Invalidate Cache using CreateInvalidationAPI

## Security Concepts
- Origin Access Identity (OAI)
- Viewer Protocol Policy
    - describes policy between client and edge location
    - redirect HTTP to HTTPS
    - or use HTTPS only
- Origin Protocol Policy
    - describes policy between cloudfront and edge location (s3 or https)
    - HTTPS only
    - or Match Viewer
    - **Note** S3 Bucket Website only support HTTP!

## CloudFront Signed URL / Signed Cookie
- use case: Distribute paid content to premium users
- Attach a policy with:
    - URL Expiration
    - IP Ranges of clients
    - Trusted Signers (List of AWS Accounts that can create Signed URLs, using AWS Console as root, by managing cloudfront keypairs on root account security credentials)
    - Trusted Key group (recommended)
        - by creating rsa 2048 bit key pairs
        - then creating key groups

- Signed URL = access to individual files
- Signed Cookies = access to multiple files

## Info Dump
- When using Cloudfront with ALB, enable the ff:
  - Forward request headers (all)
    - ensure cloudfront does not cache responses from authenticated requests
- Cookie Forwarding  (all)
    - ensures that cloudfront forwards all authentication cookies to ALB