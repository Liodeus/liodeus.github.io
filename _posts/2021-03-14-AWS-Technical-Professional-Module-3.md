---
layout: post
title: AWS Technical Professional - Module 3 - From Services to Solutions
tags: [AWS, Security, Cloud]
description: "AWS Technical Professional - Module 3 - From Services to Solutions"
---

# Table of contents

- [AWS Technical Professional - Module 3 : From Services to Solutions](#aws-technical-professional---module-3--from-services-to-solutions)
  - [The Six R's](#the-six-rs)
  - [Rehost : lift and shift](#rehost--lift-and-shift)
  - [Replatform : lift, tinker, and shift](#replatform--lift-tinker-and-shift)
  - [Refactor : modernize](#refactor--modernize)
  - [Other strategies](#other-strategies)
    - [Retire](#retire)
    - [Retain/Revisit](#retainrevisit)
    - [Repurchase](#repurchase)
  - [Cloud Architecture Best Practices](#cloud-architecture-best-practices)
    - [Design for failure and nothing fails](#design-for-failure-and-nothing-fails)
    - [Build security in every layer](#build-security-in-every-layer)
    - [Leverage different storage options](#leverage-different-storage-options)
    - [Implement elasticity](#implement-elasticity)
    - [Think parallel](#think-parallel)
    - [Loose coupling sets you free](#loose-coupling-sets-you-free)
    - [Don't fear constraints](#dont-fear-constraints)
  - [Well-Architected Framework](#well-architected-framework)
  - [The Five Pillars](#the-five-pillars)
    - [Operational excellence](#operational-excellence)
    - [Security](#security)
    - [Reliability](#reliability)
    - [Performance efficiency](#performance-efficiency)
    - [Cost Optimization](#cost-optimization)
  - [Cost optimization](#cost-optimization)
  - [Customer Use Cases](#customer-use-cases)

# AWS Technical Professional - Module 3 : From Services to Solutions

## The Six R's

- Rehost
- Replatform
- Refactor
- Retire
- Retain
- Repurchase

## Rehost : lift and shift

Transfer of application resources from an on-premises datacenter to the AWS cloud. This is a functional recreation of the on-premises network, only hosted on AWS. The customer benefits from the pay-as-you-go model, and can rapidly deploy more resources as needed.

![](/assets/imgs/AWS/lift_shift.PNG)

## Replatform : lift, tinker, and shift

It's similar to rehosting, in that the core architecture of the application isn't being changer. It's about making targeted cloud optimizations.

Examples : 

- Migrating databases to Amazon RDS
- Migrating applications to Amazon Elastic Beanstalk

![](/assets/imgs/AWS/lift_tinker_shift.PNG)

## Refactor : modernize

Re-imagining how the application is architected and developed, typically using cloud-native features.

Examples :

- Changing a database structure from an EC2-hosted database or a standard RDS database, to Amazon Aurora
- Changing a monolithic application architecture to a more service-oriented design to make use of modern technologies such as containers or serverless like AWS Lambda

![](/assets/imgs/AWS/refactor.PNG)

## Other strategies

### Retire

- Shutting off non-useful applications
- Reducing spend, management, and security

### Retain/Revisit

- Keeping certain applications on-premises

### Repurchase

- Moving workflows to software as a service (SaaS)

## Cloud Architecture Best Practices

### Design for failure and nothing fails

Assume everything fails and design backwards.

- Avoid single points of failure
- Multiple instances
- Multiple Availability Zones (AZ)
- Separate single server into multiple tiered application
- For Amazon RDS, use Multi-AZ feature

### Build security in every layer

- Encryption Data at rest an in transit
- Enforce principle of least privilege in IAM
- Implement both Security Groups and Network Access Lists (NACL)
- Consider advanced security features and services such as Amazon Inspector and Amazon Guard Duty and AWS Shield

### Leverage different storage options

- Move static web assets to Amazon S3
- Use Amazon CloudFront to serve globally
- Store session state in DynamoDB
- Use ElasticCache between hosts and databases

### Implement elasticity

- Implement Auto Scaling policies
- Architect resiliency to reboot and relaunch
- Leverage managed services like Amazon S3 and Amazon DynamoDB

### Think parallel

- Scale horizontally, not vertically, meaning add more compute resources to your application, rather than adding more power to your compute resources
- Decouple compute from session/state data, to help with scaling, and availability
- Use Elastic Load Balancing
- Righ-size your infrastructure, to get the best balance between cost and performance

### Loose coupling sets you free

When services are loosely coupled, they can scale and be made fault tolerant independently of each other.

- Instead of single, ordered workflow, use multiple queues
- Use Amazon Simple Queue Service and Simple Notification Service (SQS and SNS)
- Leverage existing services

### Don't fear constraints

Rethink traditional constraints

Need more RAM ? :  A traditional solution is to install more RAM into the application server. Instead consider distributing load across a number of commodity instances.

Better Input/Output Operations per Second (IOPS) for databases ? : A traditional solution is to painstakingly rework a relational schema to increase IOPS. Consider scaling horizontally by spreading the load around. Consider creating a read replica for your database and modifying your application to separate database read from writes.

Response to failure ? : Rather than wasting valuable time and resources diagnosing problems and replacing components, favor a "rip and replace" approach : simply decommission the entire component and spin up fully-function replacement.

## Well-Architected Framework

- A framework for ensuring infrastructures are :
  - Secure 
  - High-performing
  - Resilient
  - Efficient
- Practices developed through reviewing customer's architectures on AWS
- Systematic approach for evaluating and implementing architectures
- Well-Architected Tool in the console

More information about Well-Architected Framework : [here](https://aws.amazon.com/architecture/well-architected/)

## The Five Pillars

### Operational excellence

Focuses on running and monitoring systems to deliver business value, and continually improving processes and procedures. Key topics include managing and automating changes, responding to events, and defining standards to successfully manage daily operations.

### Security

Focuses on protecting information & systems. Key topics include confidentiality and integrity of data, identifying and managing who can do what with privilege management, protecting systems, and establishing controls to detect security events.

### Reliability

Focuses on the ability to prevent, and quickly recover from failures to meet business and customer demand. Key topics include foundational elements around setup, cross project requirements, recovery planning, and how we handle change.

### Performance efficiency

Focuses on using IT and computing resources efficiently. Key topics include selecting the right resource types and sizes based on workload requirements, monitoring performance, and making informed decisions to maintain efficiency as business needs evolve.

### Cost Optimization

Focuses on avoiding un-needed costs. Key topics include understanding and controlling where money is being spent, selecting the most appropriate and right number of resource types, analyzing spend over time, and scaling to meet business needs without overspending.

## Cost optimization

Pay for what you **need** !

- Right-sizing instances
- Increasing elasticity
- Choosing the right pricing model
- Optimizing storage

## Customer Use Cases

Key resource for finding use cases to help inspire solution design : [https://aws.amazon.com/solutions/case-studies/](https://aws.amazon.com/solutions/case-studies/)

Provides customers who need help deploying an AWS Solution by highlighting AWS Competency Partener Solutions : [https://aws.amazon.com/solutions/consulting-offers/](https://aws.amazon.com/solutions/consulting-offers/)

Quick Starts are built by AWS solutions architecs and partners to help you deploy popular technologies on AWS, based on AWS best practices for security and high availability : [https://aws.amazon.com/quickstart/](https://aws.amazon.com/quickstart/)

