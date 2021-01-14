---
layout: post
title: Identity and Access Management- CISSP
tags: [CISSP, CHAPTER_5, Identity and Access Management]
description: "Identity and Access Management - Chapter 5"
---

# Identity and Access Management (IAM)

## Access controls

Access : is the flow of information between a subject and an object.

Subject : is an active entity that requests access to an object or the data within an object.

Object : is a passive entity that contains information or needed functionality.

Control : security measures taken to restrict or allow access to systems.

## Security principles

- Availability
- Integrity
- Confidentiality

## Identity management

IAAA - **I**dentification - **A**uthentication - **A**uthorization - **A**ccountability

Identification : method by which a subject claims to have a specific identity. Example : username, account number, e-mail address.

Authentication : process by which a system verifies the identity of the subject. Example : password, passphrase, cryptographic key, PIN.

Authorization : defining resources for user access

Accountability : person responsible for the controls, uses logs.

## Identification and authentication

Authentication by knowledge : something a person knows.

Authentication by ownership : something a person has.

Authentication by characteristic : something a person is.

Strong authentication or multifactor authentication (MFA) : must contains two or all of the three methods, something a person knows, has or is.

### Secure identities key aspects

- Uniqueness
  - Refers to the identifiers that are specific to an individual, meaning every user must have a unique ID for accountability.
- Non-descriptive
  - Neither piece of the credential set should indicate the purpose of the account.
- Issuance
  - Elements that have been provided by another authority as a means of proving identity (ID cards).





![](/assets/imgs/CISSP/CH05/)











## Data access controls

- Discretionary access controls (DAC)
  - Each resource object on a DAC based system has an *Access Control List* (ACL) associated with it. An ACL contains a list of users and groups to which the user has permitted access together with the level of access  for each user or group. For example, *User A* may provide read-only access on one of her files to *User B*, read and write access on the same file to *User C* and full control to any user belonging to *Group 1*.
- Mandatory access controls (MAC)
  - MAC takes a hierarchical approach to controlling access to resources. Under a MAC enforced environment access to all resource objects (such as data files) is controlled by settings defined by the system  administrator. As such, all access to resource objects is strictly  controlled by the operating system based on system administrator  configured settings. It is not possible under MAC enforcement for users  to change the access control of a resource.
- Non-discretionary access controls / Role Based Access Control (RBAC)
  - Enables the assignment of file permissions, such as read, write and execute, to regulate access to data objects. However, only an administrator can set and modify the permissions. Essentially, RBAC assigns permissions to particular roles in an organization. Users are then assigned to that particular role. For example, an accountant in a company will be assigned to the *Accountant* role, gaining access to all the resources permitted for all accountants on the system.