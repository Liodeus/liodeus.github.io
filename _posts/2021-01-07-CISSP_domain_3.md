---
layout: post
title: Security Architecture and Engineering - CISSP
tags: [CISSP, CHAPTER_3, Security Architecture and Engineering]
description: "Security Architecture and Engineering - Chapter 3"
---

# Security Architecture and Engineering

## System architecture

Architecture : describes the major components of the system and how they interact with each other, with the users, and with other systems.

Development : refers to the entire life cycle of a system, including the planing analysis, design, building, testing, deployment, maintenance, and retirement phases.

 ISO/IEC/IEEE 42010:2011 : Recommended Practice for Architectural Description of Software-Intensive Systems.

Architecture description (AD) : Collection of document types to convey an architecture in a formal manner.

Stakeholder : Individual, team, or organization with interests in, or concerns relative to, a system.

View : Representation of a whole system from the perspective of a related set of concerns.

Viewpoint : A specification of the conventions for constructing and using a view. A template from which to develop individual views by establishing the purposes and audience for a view and the techniques for its creation and analysis.





















## Encryption

### Symmetric

Symmetric encryption aka secret key encryption uses one single key to encrypt and decrypt data. You have to share this key with the recipient. Symmetric encryption algorithms are computationally faster than asymmetric encryption algorithms. For examples : DES, 3DES, AES, RC4, etc.

![Symmetric Encryption](https://www.ssl2buy.com/wiki/wp-content/uploads/2015/12/Symmetric-Encryption.png)

### Asymmetric

Asymmetric encryption requires two keys to work. Firstly, a public key must be made public in order to encrypt the data. Secondly, a private key used to decrypt the data. For examples : RSA, Diffie-Hellman, DSA, etc.

![Asymmetric Encryption](https://www.ssl2buy.com/wiki/wp-content/uploads/2015/12/Asymmetric-Encryption.png)

## Bell-LaPadula model (BLP)

The Bell-LaPadula security model is directed toward access control and is characterized by the phrase "no read up, no write down". It enforces the confidentiality aspects of access control. A system that employs the Bell-LaPadula model is called a multilevel security system because users with different clearances use the system, and the system processes data at different classification levels.

Three main rules are used and enforced in the Bell-LaPadula model:

- Simple security rule
  - A subject at a given security level cannot read data that resides at a higher security level.
- *-property (star property) rule
  - A subject in a given security level cannot write information to a lower security level.
- Strong star property rule
  - Subject who has read and write capabilities can only perform both of those functions at the same security level; nothing higher and nothing lower.

![Access Control](https://www.cs.rutgers.edu/~pxk/419/notes/images/bell-lapadula.png)

## Biba model

The Biba model is a security model that addresses the integrity of data within a system and is characterized by the phrase "no read down, no write up". It is not concerned with security levels and confidentiality. The Biba model uses integrity levels to prevent data at any integrity level from flowing to a higher integrity level. Biba has three main rules to provide this type of protection:

- *-integrity axiom
  - A subject cannot write data to an object at a higher integrity level (referred to as “no write up”).
- Simple integrity axiom
  - A subject cannot read data from a lower integrity level (referred to as “no read down”).
- Invocation property
  - A subject cannot request service (invoke) at a higher integrity.

## Lipner model

Combines the elements of BPL and Biba model to provide confidentiality and integrity.

Lipner = BPL + Biba

## Clark-Wilson model

The Clark-Wilson model is for upholding integrity. A distinctive feature of the Clark-Wilson model is that it focuses on well-formed transactions and separation of duties. A well-formed transaction is a series of operations that transform a data item from one consistent state to another. Think of a consistent state as one wherein we know the data is reliable. This consistency ensures the integrity of the data and is the job of the TPs. Separation of duties is implemented in the model by adding a type of procedure (the IVPs) that audits the work done by the TPs and validates the integrity of the data.

This model uses the following elements:

- Users
  - Active agents
- Transformation procedures (TPs)
  - Programmed abstract operations, such as read, write, and modify
- Constrained data items (CDIs)
  - Can be manipulated only by TPs
- Unconstrained data items (UDIs)
  - Can be manipulated by users via primitive read and write operations
- Integrity verification procedures (IVPs)
  - Check the consistency of CDIs with external reality

![https://static.wixstatic.com/media/dc6afa_d1767a0807e34c8d96f7a561024c0c15~mv2.png/v1/fit/w_1000%2Ch_1000%2Cal_c%2Cq_80/file.png](https://static.wixstatic.com/media/dc6afa_d1767a0807e34c8d96f7a561024c0c15~mv2.png/v1/fit/w_1000%2Ch_1000%2Cal_c%2Cq_80/file.png)

## Noninterference model

This concept is implemented to ensure any actions that take place at a higher security level do not affect, or interfere with, actions that take place at a lower level. This type of model does not concern itself with the flow of data, but rather with what a subject knows about the state of the system. So, if an entity at a higher security level performs an action, it cannot change the state for the entity at the lower level. If a lower-level entity was aware of a certain activity that took place by an entity at a higher level and the state of the system changed for this lower-level entity, the entity might be able to deduce too much information about the activities of the higher state, which, in turn, is a way of leaking information.

## Chinese Wall / Brewer and Nash model

The Brewer and Nash model, also called the Chinese Wall model, states that a subject can write to an object if, and only if, the subject cannot read another object that is in a different dataset. It was created to provide access controls that can change dynamically depending upon a user’s previous actions. The main goal of the model is to protect against conflicts of interest by users’ access attempts.

![https://www.personal.psu.edu/gms/sp09/456/chinese-wall.jpg](https://www.personal.psu.edu/gms/sp09/456/chinese-wall.jpg)

## Graham-Denning model

This model addresses the security issues associated with how to define a set of basic rights on how specific **subjects** can execute security functions on an **object**. The model has eight basic protection **rules** (actions) that outline :

- How to securely create an object.
- How to securely create a subject.
- How to securely delete an object.
- How to securely delete a subject.
- How to securely provide the read access right.
- How to securely provide the grant access right.
- How to securely provide the delete access right.
- How to securely provide the transfer access right.

Moreover, each object has an owner that has special rights on it, and each subject has another subject (controller) that has special rights  on it.

## Harrison-Ruzzo-Ullman (HRU) model

The Harrison-Ruzzo-Ullman (HRU) model deals with access rights of subjects and the integrity of those rights. A subject can carry out only a finite set of operations on an object. Since security loves simplicity, it is easier for a system to allow or disallow authorization of operations if one command is restricted to a single operation.