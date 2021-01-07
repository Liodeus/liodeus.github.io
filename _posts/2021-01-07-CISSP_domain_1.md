---
layout: post
title: Security and Risk Management
tags: [CISSP, CHAPTER_1, Security and Risk Management]
description: "Security and Risk Management - Chapter 1"
---

# Security and Risk Management

![What is the CIA triad? - Comtact](https://www.comtact.co.uk/wp-content/uploads/2020/06/What-is-the-CIA-triad_431804671-550x500px.png)

Availability : ensures reliability and timely access to data and resources to authorized individuals.

Integrity : is the assurance of the accuracy and reliability of information and systems is provided and any unauthorized modification is prevented.

Confidentiality : ensures that the necessary level of secrecy if enforced at each junction of data processing and prevents authorized disclosure.

### **Availability**

- Redundant array of independent disks (RAID)
- Clustering
- Load balancing
- Redundant data and power lines
- Software and data backups
- Disk shadowing
- Co-location and offsite facilities
- Rollback functions
- Fail-over configurations (**Failover** is the ability to seamlessly and automatically switch to a reliable backup system.)

### **Integrity**

- Hashing (data integrity)
- Configuration management (system integrity)
- Change control (process integrity)
- Access control (physical integrity)
- Software digital signing
- Transmission cyclic redundancy check (CRC) functions

### **Confidentiality**

- Encryption for data at rest (whole disk, database encryption)
- Encryption for data in transit (IPSec, TLS, PPTP, SSH)
- Access control (physical and technical)

## Security definitions

Vulnerability : is a weakness in a system that allows a threats source to compromise its security.

Threat : is any potential danger that is associated with the exploitation of a vulnerability.

Risk : is the likelihood of a threat source exploiting a vulnerability and the corresponding business impact.

Exposure : is an instance of being exposed to loss.

Control : or countermeasure, is to put into place to mitigate (reduce) the potential risk.

![](/assets/imgs/CISSP/CH01/one.PNG)

## Control types

- Administrative
  - "Soft controls" -> examples : security documentation, risk management, etc.
- Technical
  - "Logical controls" -> examples : software or hardware components as in firewalls, IDS, encryption, etc.
- Physical
  - items put into place to protect facilities, personnel, and resources -> example : locks, fencing, lighting, etc.

Defense-in-depth : is the coordinated use of multiple security controls in a layered approach.

![](/assets/imgs/CISSP/CH01/Defense-in-Depth-Graphic.png)

The rule of thumb is the more sensitive the asset, the more layers of protection that must be put into place.

## Access controls

There are seven categories of access controls. The following are the seven categories of access controls :

- Deterrent
  - Intended to discourage a potential attacker.
- Preventive
  - Intended to avoid an incident from occurring.
- Compensating
  - Controls that provide an alternative measure of control.
- Detective
  - Helps identify an incident's activities and potentially an intruder.
- Corrective
  - Fixes components or systems after an incident has occurred.
- Recovery
  - Intended to bring the environment back to regular operations.

When looking at a security structure of an environment, it is most productive to use a preventive model and then use detective, corrective, and recovery mechanisms to help support this model.

It is not feasible to prevent everything; therefore, what you cannot prevent, you should be able to quickly detect.

![](/assets/imgs/CISSP/CH01/two.PNG)























## Risk mitigation

Risk mitigation is a strategy to prepare for and lessen the effects of  threats faced by a business. Risk mitigation takes steps to reduce the negative effects of threats and disasters on business continuity.

Acceptable risk responses:

-  Reduction/mitigation
  - Take an action that should reduce the impact or the probability of the risk to an acceptable level. The acceptable level is called a **Residual Risk Level**.
- Transfer
  - Describes situation when we transfer the risk to **another** person or entity such as insurance agency. SLAs (Service Level Agreements) and contracts establish the degree of transference.
- Acceptance
  - We will not take any action because we can accept its **impact** and **probability** - we simply **risk it**. It is determined the cost of the control is less than the potential for loss
- Avoidance
  - Should be performed whenever the costs of mitigating or accepting a risk are higher than the benefits gained by providing the service.

## Disaster recovery (DR) site

- Mutual assistance agreement (MAA)

  - A Mutual Assistance Agreement or MAA is  an arrangement between two or more companies such that each will assist  the other in the event of a disaster, typically by sharing computing  resources. 

    Care should be taken in such agreements to ensure that the two companies are unlikely to be victims of the same disaster. e.g. they should not  be too physically close to each other or lie on the same earthquake  fault zone.

- Hot site

  - A hot site is a backup facility which represents a mirrored copy of  the primary production center. A hot site is equipped with all the  necessary hardware, software, and network connectivity, which allows you to perform near real-time backup or replication of the critical data.  This way the production workload can be failed over to a DR site in a  few minutes or hours, thus ensuring minimal downtime and zero data loss. A hot site is expected to be always online and running without  disruption so as to ensure data synchronization between the sites.

    It is  important to ensure that this type of a DR site is located far enough  from the production center. This way you can decrease the possibility of a hot site being affected by the same disaster as the primary site.

- Warm site

  - A warm site is considered the middle ground between the cold site and  the hot site. A warm site is a backup facility that has the network  connectivity and the necessary hardware equipment already pre-installed. However, a warm site cannot perform on the same level as the production center because they are not equipped in the same way. Therefore, a warm site has less operational capacity than the primary site. Moreover,  data synchronization between the primary and the secondary sites is  performed daily or weekly, which can result in minor data loss. A warm  site is perfect for organizations which operate with less critical data  and can tolerate a short period of downtime

- Cold site

  - A cold site is a backup facility with little or no hardware equipment  installed. A cold site is essentially an office space with basic  utilities such as power, cooling system, air conditioning, and  communication equipment, etc. A cold site is the most cost-effective  option among the three disaster recovery sites. However, due to the fact that a cold site doesn’t have any pre-installed equipment, it takes a  lot of time to properly set it up so as to fully resume business  operations. In case of a disaster, an organization would require help  from IT personnel to migrate necessary servers and make them functional  in order to take on the workload of the primary site.

## Issue Specific Policies

### Change Management Policy

 In order to maintain consistent and known operational security, a regimented change management or change control process needs to be followed. The purpose of the change control process is to understand, communicate, and document any changes with the primary goal of being able to understand, control, and avoid direct or indirect negative impact that the change might impose.

The general flow of the change management process includes:

- Identifying a change
- Proposing a change
- Assessing the risk associated with the change
- Testing the change
- Scheduling the change
- Notifying impacted parties of the change
- Implementing the change
- Reporting results of the change implementation

All changes must be closely tracked and auditable; a detailed change record should be kept.

### Acceptable Use Policy

How can you use company resources.

### Privacy

Notification

### Data/System Ownership

Make sure it's clear who owns the systems or the data.

### Separation of Duties (SOD)

No one in the organization have to much power/authority.

### Mandatory Vacations

Detective control.

### Job Rotation

Detective control and also redundancy.

### Least privilege

About action, it's about what can you do.

### Need to know

About data rights or permissions.

### Dual control

Preventing abuse of power.

### M of N control

Not being bound to a number of persons (more flexible than Dual control).



![http://3.bp.blogspot.com/-QaufMsSHYnw/Uv2_ue4_vTI/AAAAAAAABJE/S4On5CWo_yc/s1600/Guidelines+Procedure+Standard+Policy+620.png](http://3.bp.blogspot.com/-QaufMsSHYnw/Uv2_ue4_vTI/AAAAAAAABJE/S4On5CWo_yc/s1600/Guidelines+Procedure+Standard+Policy+620.png)

| Document  | Example                                                      | Mandatory or Discretionary |
| --------- | ------------------------------------------------------------ | -------------------------- |
| Policy    | Protect the CIA of PII by hardening the operating system     | Mandatory                  |
| Procedure | Step 1: Install prehardened OS image.<br />Step 2: Download patches from update server.<br />Step 3: ... | Mandatory                  |
| Standard  | Use Nexus-6 laptop hardware                                  | Mandatory                  |
| Guideline | Patch installation may be automated via the use of an installer script | Discretionary              |
| Baselines | Use the CIS Security Benchmarks Windows Benchmark            | Discretionary              |

https://workbench.cisecurity.org



## Risk Definition

- Asset : Anything of value to the company
- Vulnerability : A weakness; the absence of a safeguard
- Threat : Something that could pose loss to all or part of an asset
- Threat agent : What carries out the attack
- Exploit : An instance of compromise
- Risk : The probability of a threat materializing
- Controls : Physical, administrative, and technical protections
  - Safeguards (proactive)
  - Countermeasure (reactive)
- Total risk : The risk that exists before any controls is implemented
- Residual risk : Leftover risk after applying a control
- Secondary risk : When one risk response triggers another risk event
  - Incident : A risk event that has transpired



Due diligence : Research

Due care : Action
