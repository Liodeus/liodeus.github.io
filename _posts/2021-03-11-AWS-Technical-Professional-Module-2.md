---
layout: post
title: AWS Technical Professional - Module 2 - AWS Core Technologies
tags: [AWS, Security, Cloud]
description: "AWS Technical Professional - Module 2 - AWS Core Technologies"
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
  - [Amazon Elastic Load Balancing (ELB)](#amazon-elastic-load-balancing-elb)
    - [Three types of ELB :](#three-types-of-elb-)
  - [Storage services](#storage-services)
  - [Amazon Elastic Block Storage](#amazon-elastic-block-storage)
  - [Amazon Simple Storage Service (Amazon S3)](#amazon-simple-storage-service-amazon-s3)
  - [Storage classes on Amazon S3](#storage-classes-on-amazon-s3)
    - [Standard](#standard)
    - [Standard Infrequent Access (Standard IA)](#standard-infrequent-access-standard-ia)
    - [One Zone Infrequent Access](#one-zone-infrequent-access)
    - [Amazon Glacier](#amazon-glacier)
    - [S3 Intelligent Tiering](#s3-intelligent-tiering)
  - [Databases services](#databases-services)
  - [EC2-hosted vs AWS Database Services](#ec2-hosted-vs-aws-database-services)
    - [AWS Database Services](#aws-database-services)
    - [Databases on Amazon EC2](#databases-on-amazon-ec2)
  - [Networking](#networking)
  - [Amazon VPC](#amazon-vpc)
  - [Securing a VPC](#securing-a-vpc)
  - [Security, Identity and Compliance services](#security-identity-and-compliance-services)
  - [Amazon Identity and Access Management (Amazon IAM)](#amazon-identity-and-access-management-amazon-iam)
  - [Cloud security on AWS](#cloud-security-on-aws)
  - [AWS management interfaces](#aws-management-interfaces)

# AWS Technical Professional - Module 2 : AWS Core Technologies

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

## Amazon Elastic Load Balancing (ELB)

**Automatically distribute traffic** across multiple EC2 instances.

- Increases availability and fault tolerance
- Configure health checks
- Offload encryption and decryption

### Three types of ELB :

- Application Load Balancer (app layer)
- Network Load Balancer (network layer)
- Classic Load Balancer (classic instances)

## Storage services

A reliable, scalable, and secure place for data.

Amazon Elastic Block Store : Persistent block-level storage

Amazon S3 : Durable, scalable object storage

Amazon S3 Glacier : Data archiving and backup

AWS Storage Gateway : Seamless and secure integration

Amazon Elastic File System : File storage for Amazon EC2 instance

## Amazon Elastic Block Storage

Network-attached block storage for use with Amazon EC2 instances. Sizes range from 1GB to 16 TB and allocated by 1GB increments.

- Persist independently from instance
- Used like a physical hard drive
- Automatically replicated
- Attached to any instance in the same AZ
- One EBS volume to EC2 instance
- One instance to many EBS volumes
- EBS volumes can retain data after EC2 instance termination
- Allow point-in-time snapshots to S3 GiB increments

## Amazon Simple Storage Service (Amazon S3)

Infinite scalability, greater analysis, and faster data retrieval. Highly scalable **object storage** with 99.99% durability and 99.99% availability.

Common S3 use cases :

- Backup and storage
- Application hosting
- Media hosting
- Software delivery

More information about S3 : [here](https://aws.amazon.com/s3/)

## Storage classes on Amazon S3

### Standard

Appropriate for a wide variety of use cases.

- Frequently access data
- Low latency and high throughput

### Standard Infrequent Access (Standard IA)

Similar to S3 Standard but with a lower per GB storage price and a per GB retrieval fee. Ideal for long term storage, backups and as a data store for disaster recovery files

- Less frequently access data, but requires rapid access when needed

### One Zone Infrequent Access

Ideal for customer who do not require the availability and resilience of  S3 Standard or S3 Standard IA, good choice for storing secondary backups copies of on premises data or easily recreatable data.

- Access data less frequently 
- Store data in a single AZ
- It cost %20 less than Standard IA

### Amazon Glacier

Secure, durable and low cost storage classes for data archiving. Three retrieval options that range to a few minutes to hours. 

### S3 Intelligent Tiering

Deliver automatic cost savings by moving data between two access tiers configures by the customer.

More information about storage classes : [here](https://aws.amazon.com/s3/storage-classes/)

## Databases services

Amazon RDS : Cost efficient and resizable capacity

Amazon DynamoDB : Fast and predictable performance

Amazon ElasticCache : Fast, managed information retrieval

More information about storage classes : [here](https://aws.amazon.com/products/databases)

## EC2-hosted vs AWS Database Services

### AWS Database Services

- Easy to set up, manage, maintain
- Reduce undifferentiated heavy lifting
- Push-button high availability
- Automatic backup/recovery
- Scale up or down based upon pattern

### Databases on Amazon EC2

- More control/flexibility
- Operating system access
- Need features of specific application

## Networking

Amazon VPC : Build a virtual network in the clound

Security Groups : Control access to insances

Network Access Control Lists (NACL) : Control access to subnets

Amazon Route 53 : Route end users to internet applications

## Amazon VPC

Networking layer for Amazon EC2. A virtual network dedicated to a customer's AWS account.

Subnet : A range of IP addresses in a VPC

Public subnets : can be used for resources that must be connected to the Internet

Private subnets : can be used for resources that wont be connected to the Internet

## Securing a VPC

Network Access Control Lists : Control traffic at the **subnet** level

Security groups : Control traffic at the **instance** level

Flow logs : Capture network flow information

Host-based firewalls : Operating system firewalls

More information about securing a VPC : [here](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html)

## Security, Identity and Compliance services

Encryption, acces management, and securing regulated workloads

AWS IAM : Securely control access

Share Responsibility Model

Cloud compliance

More information about security, Identity and Compliance : [here](https://aws.amazon.com/products/security/)

## Amazon Identity and Access Management (Amazon IAM)

Securely manage access to AWS services and resources

- Fine-grained access control to AWS resources
- Multi-factor authentication
- The ability to analyze access
- Integration with corporate directories

More information about Amazon IAM : [here](https://aws.amazon.com/iam/)

## Cloud security on AWS

- Inherit benefits from AWS data center and network architecture
- Similar to on premises data centers, without maintaining facilities and hardware
- Can be esaily automated
- Inherit all the best practices of AWS

## AWS management interfaces

AWS Management Console : Graphical interface to facilitate cloud management

Command Line Interface (AWS CLI) : Access to services via discrete command

Software Development Kits (SDKs) : Access services in your code