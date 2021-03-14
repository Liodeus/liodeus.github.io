---
layout: post
title: AWS Technical Professional - Module 3 - From Services to Solutions
tags: [AWS, Security, Cloud]
description: "AWS Technical Professional - Module 3 - From Services to Solutions"
---

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