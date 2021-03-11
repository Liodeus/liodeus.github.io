---
layout: post
title: AWS Technical Professional
tags: [AWS, Security, Cloud]
description: "AWS Technical Professional"
---

# Table of contents

- [AWS Technical Professional](#aws-technical-professional)
  - [Advantages of cloud computing](#advantages-of-cloud-computing)
  - [AWS products](#aws-products)
  - [AWS Global Infrastructure](#aws-global-infrastructure)
    - [AWS : Regions](#aws--regions)
    - [AWS : Availability Zones (AZ)](#aws--availability-zones-az)
    - [AWS : Points of Presence (PoP)](#aws--points-of-presence-pop)
  - [Compute Services](#compute-services)
  - [Amazon EC2 choices : Instance Types](#amazon-ec2-choices--instance-types)
  - [Amazon Machine Images (AMI)](#amazon-machine-images-ami)
    - [Public images](#public-images)
      - [Paid images](#paid-images)
      - [Private images](#private-images)
  - [Why Scaling Matters](#why-scaling-matters)
  - [Amazon EC2 : Auto Scaling](#amazon-ec2--auto-scaling)

# AWS Technical Professional

## Advantages of cloud computing

1. Trade capital expense for variable expense
2. Benefit from massive economies of scale
3. Stop guessing capacity
4. Increase speed and agility
5. Stop spending money running and maintaining data centers
6. Go global in minutes

## AWS products

Products available in **seconds**, with **pay-as-you-go** pricing :

- Compute
- Storage
- Databases
- Analytics
- Networking
- Mobile
- Developer tools
- Management tools
- IoT
- Enterprise apps
- Security

## AWS Global Infrastructure

### AWS : Regions

Resources are hosted on multiple location worldwide, called **AWS region**.

Each region is completely isolated from each other, this achieve the greatest fault tolerance and stability.

### AWS : Availability Zones (AZ)

Each AZ is isolated from other AZs within a region. Though physically separated all AZ within a region are interconnected via a high bandwidth, low latency, fully redundant fiber.

### AWS : Points of Presence (PoP)

Consist of edge locations and regional edge cache servers. This location are used to securely deliver :

- Data
- Videos
- Applications
- API

With low latency and high transfer speeds. More information about current presence : [here](https://aws.amazon.com/about-aws/global-infrastructure/)

## Compute Services

Develop, deploy, run, and scale workloads in the AWS Cloud.

- Amazon EC2 : Resize compute capacity
- Amazon EC2 Auto Scaling : Increase or decrease number of instances
- Elastic Load Balancing : Distribute incoming traffic
- AWS Lambda : Run code in response to events
- Amazon Elastic Container Service : Run applications on a managed cluster

More information about compute services : [here](https://aws.amazon.com/products/compute/)

## Amazon EC2 choices : Instance Types

More information about instance types : [here](https://aws.amazon.com/ec2/instance-types/)

## Amazon Machine Images (AMI)

### Public images

These are machine images that are safe, secure and customized for public consumption. 

#### Paid images

These are images that can be purchased from a developer. EC2  users can purchase the images from the AWS Marketplace, an online store  that sells software running on Amazon Web Services.

#### Private images 

A private machine image can only be used by EC2 users who have been granted access to it by the developer. 

## Why Scaling Matters

- Launch new instances in advance of peak periods
- Use monitoring to programmatically scale out
- Automatically scale in
- Pay for the resources needed, when needed

## Amazon EC2 : Auto Scaling

**Automatically add** or **remove** instances to **adapt to demand** :

- Monitor the health of running instances
- Replace impaired instances automatically
- Balance capacity across availability zones
- Dynamic and predictive scaling