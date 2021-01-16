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

 is a networking protocol for clock synchronization between computer systems, it uses UDP on port 123.

![](/assets/imgs/CISSP/CH06/two.PNG)

Stratum 0 : Highly accurate time sources

Stratum 1 : Primary time source

Stratum 2 : Local network servers

Stratum 3 : Any other servers

