---
layout: post
title: Security Assessment and Testing - CISSP
tags: [CISSP, CHAPTER_5, Security Assessment and Testing]
description: "Security Assessment and Testing - Chapter 6"
---

# Security Assessment and Testing

Test : is a procedure that records some set of properties or behaviors in a system being tested and compares them against predetermined standards.

Assessment : is a series of planned tests that are somehow related to each other.

Audit : is a systematic assessment of significant importance to the organization that determines whether the system or process being audited satisfies some external standards.

## Information System Security Audit Process

1. Determine the goals, because everything else hinges on this.
2. Involve the right business unit leaders to ensure the needs of the business are identified and addressed.
3. Determine the scope, because not everything can be tested.
4. Choose the audit team, which may consist of internal or external personnel, depending on the goals, scope, budget, and available 
5. expertise.
6. Plan the audit to ensure all goals are met on time and on budget.
7. Conduct the audit while sticking to the plan and documenting any deviations therefrom.
8. Document the results, because the wealth of information generated is both valuable and volatile.
   Communicate the results to the right leaders in order to achieve and sustain a strong security posture.

## Conducting Internal Audits

Internal audit : is an audit conducted by an internal team.

- Mark your calendars
- Prepare the auditors
- Document everything
- Make the report easy to read

## Conducting and Facilitating External Audits

External audit : is an audit conducted by or on behalf of a business partner.

- Learn the contract
- Schedule in and out briefs
- Travel in pairs
- Keep it friendly

## Facilitating Third-Party Audits

Signing a nondisclosure agreement is almost always a prerequisite before a third-party team is permitted to audit an organization's system.

- Know the requirements
- Pre-audit
- Lock in schedules
- Get organized
- Keep the boss informed

## Test Coverage

Is a measure of how much of a system is examined by a specific test, which is typically expressed as a percentage.

## Auditing Technical Controls

Is a security control implemented through the use of an IT asset. This asset is usually, but not always, some sort of software that is configured in a particular way. When we audit our technical controls, we are testing their ability to mitigate the risks that we identified in our risk management process.

## Vulnerability Testing and Penetration Testing (Pentest)

Vulnerability testing : is the act of identifying potential vulnerabilities in network devices such as firewalls, routers, switches, servers and applications. It is automated and focuses on finding potential and known vulnerabilities on the network or an application level, it does not exploit the vulnerabilities.

Before carrying out vulnerability testing or a pentest, a written agreement from management is required ! This protects the tester against prosecution for doing his job and ensures there are no misunderstandings bu providing in writing what the tester should and should not do.

- Evaluate the true security posture of an environment
- Identify as many vulnerabilities as possible
- Test how systems react to certain circumstances and attacks
- Before the scope of the test is decided and agreed upon, the tester must explain the testing ramifications

Penetration testing : is the process of simulating attacks on network and its systems. It emulates the same methods attackers would use, there is no automated penetration testing it requires the use of tools and an experienced person to conduct it.

### Various types of assessments

- Personnel testing
  - Reviewing employee tasks and thus identifying vulnerabilities in the standard practices and procedures that employees are instructed to follow.
- Physical testing
  - Reviewing facility and perimeter protection mechanisms.
- System and network testing
  - Identifies known system vulnerabilities.

### Box color

- Black box
  - Treats the system as completely opaque, the tester has no prior knowledge of the internal design or features of the system.
  - Disadvantage : do not cover all of the internal controls, the test team may inadvertently target a subsystem that is critical.
- White box (crystal box)
  - Affords the auditor complete knowledge of the inner working of the system.
  - Disadvantage : may not be representative of the behaviors of an external attacker.
- Gray box
  - Some but not all, information on the internal workings is provided to the test team.

## War Dialing

Allows attackers and administrators to dial large blocks of phone numbers in search of available modems.

## Example of a testing schedule that each operations and security department should develop and carry out

![](/assets/imgs/CISSP/CH06/one.PNG)

## Log Reviews

Is the examination of system log files to detect security events or to verify the effectiveness of security controls.

### Preventing Log Tampering

- Remote logging
- Simplex communication
- Replication
- Write-once media
- Cryptographic hash chaining

Security information and event managers (SIEM) : systems that enable the centralization, correlation, analysis and retention of event data in order to generate automated alerts.

## Network Time Protocol (NTP)

Is a networking protocol for clock synchronization between computer systems, it uses UDP on port 123.

![](/assets/imgs/CISSP/CH06/two.PNG)

Stratum 0 : Highly accurate time sources

Stratum 1 : Primary time source

Stratum 2 : Local network servers

Stratum 3 : Any other servers

## Synthetic Transaction

Is a monitoring technique that is done by using an emulation or scripted recordings of transactions.

## Real User Monitoring (RUM)

Is a passive way to monitor the interactions of real users with a web application or system. It uses agents to capture metrics such as delay, jitter, and errors from the user's perspective.

## Code Review Process

1. **Identify the code** to be reviewed
   - Usually a specific function or file.
2. **Organizes the inspection**
  - And makes sure everyone has access to the correct version of the source code, along with all supporting artifacts.
3. **Prepares for inspection**
  - By reading through the code and making notes.
4. All the obvious errors are **collated offline**
  - Not in a meeting so they don’t have to be discussed during the inspection meeting (which would be a waste of time).
5. If everyone **agrees the code is ready for inspection**, then the meeting goes ahead.
6. Everyone **discusses bugs**
  - Design issues, and anything else that comes up about the code. A scribe (not the author of the code) writes everything down.
7. **Disposition of code**, at the end of the meeting, everyone agrees on :
  - Passed : Code is good to go
  -  Passed with rework : Code is good so long as small changes are fixed
  -  Reinspect : Fix problems and have another inspection
8. **Fixes** any mistakes and checks in the new version.
9. If the disposition of the code in step 7 was passed with rework, the team leader checks off the bugs that the scribe wrote down and makes sure they’re all fixed.
10. If the disposition of the code in step 7 was reinspect, the team leader goes back to step 2 and starts over again.

## Auditing Administrative Controls

### Adding Accounts

**All** new users should be required to **read** through and **acknowledge** they understand (by signing) all policies that apply to them. At a minimum, every organization should have (and every user should **sign**) an **acceptable use policy** (AUP) that specifies what the organizations considers acceptable use of the information system that are made available to the employee.

Testing that all employees are aware of the AUP and other applicable policies can be the first step in auditing user accounts. Since every user should have a signed AUP, for instance, all we need is to get a list of all users in the organization and then compare it to the files containing the signed documents.

The policies also should dictate the default expiration date of accounts, the password policy, and the information to which a user should have access.

### Modifying Accounts

Adding, removing, or modifying the permissions that a user has should be a carefully controlled and documented process.

- When are the new permissions effective ? 
- Why are they needed ?
-  Who authorized the change ? 

Organizations that are mature in their security processes will have a change control process in place to address user privileges. While many auditors will focus on who has administrative privileges in the organization, there are many custom sets of permissions that approach the level of an admin account. It is important, then, to have and test processes by which elevated privileges are issued.

### Suspending Accounts

Whatever the reason, we must ensure that the account of someone who is not present to use it is suspended until that person returns or the term of our retention policy is met.

Testing the administrative controls on suspended accounts follows the same pattern already laid out in the preceding two sections: look at each account (or take a representative sample of all of them) and compare it with the status of its owner. Alternatively, we can get a list of employees who are temporarily or permanently away from the organization and check the status of those accounts. It is **important** that accounts are deleted **only in strict** accordance with the data retention policy.

## Backup Verification

The frequency of each backup (hourly, daily, weekly) is driven by the risk management process. Whatever the approach to backing up data, we need to **periodically test** it to ensure that the backups will work as promised when we need them.

**Never backup** your data to the same device on which the original data exists.

### Types of Data

- User Data Files
- Databases
- Mailbox Data

### Testing Data Backups

- **Develop scenarios** that capture specific sets of events that are representative of the threats facing the organization.
- **Develop a plan** that tests all the mission-critical data backups in each of the scenarios.
- **Leverage automation** to minimize the effort required by the auditors and ensure tests happen periodically.
- **Minimize impact on business** processes of the data backup test plan so that it can be executed regularly.
- **Ensure coverage** so that every system is tested, though not necessarily in the same test.
- **Document the results** so you know what is working and what needs to be worked on.
- **Fix or improve** any issues you documented.

## Disaster Recovery and Business Continuity

Business Continuity Plan (BCP) : The overall organizational plan for "how-to" continue business.

Disaster Recovery Plan (DRP) : The plan for recovering from an IT disaster and having the IT infrastructure back in operation.

### Testing and Revising the Business Continuity Plan

#### Checklist test or Desk check test

- Copies of the DRP or BCP are distributed to the different departments for review
- Once the departments have reviewed their copies and made suggestions, the planning team then integrates those changes into the master plan.

#### Structured Walk-Through test

- Representatives from each department or functional area come together and go over the plan to ensure its accuracy.
- The group reviews the objectives of the plan.
- Discusses the scope and assumptions of the plan.
- Reviews the organization and reporting structure.
- Evaluates the testing, maintenance, and training requirements described.
- The group walks through different scenarios of the plan from beginning to end to make sure nothing was left out.

#### Tabletop exercises (TTXs)

The key personnel who have emergency management roles and responsibilities gather together to discuss various simulated  emergency situations. Because the environment of a tabletop is  non-threatening (i.e., a “real” emergency is not happening), the people  gathered together around the table can calmly rehearse their roles, ask  questions, and troubleshoot problem areas.

#### Simulation test

All employees who participate in operational and support functions, or their representatives, come together to practice executing the disaster recovery plan based on a specific scenario. The scenario is used to test the reaction of each operational and support representative.

The drill includes only those materials that will be available in an actual disaster to portray a more realistic environment. The simulation test continues up to the point of actual relocation to an offsite facility and actual shipment of replacement equipment.

#### Parallel test

Some systems are moved to the alternate site and processing takes place. The results are compared with the regular processing that is
done at the original site. This ensures that the specific systems can actually perform adequately at the alternate offsite facility, and points out any tweaking or reconfiguring that is necessary.

#### Full-Interruption test

The original site is actually shut down, and processing takes place at the alternate site. The recovery team fulfills its obligations in preparing the systems and environment for the alternate site. All processing is done only on devices at the alternate offsite facility.

Full-interruption tests should be performed **only** after all other types of tests have been successful.