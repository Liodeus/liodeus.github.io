---
layout: post
title: Jenkins - Vulnerabilities analysis part 3
tags: [Jenkins, Security, CI, CD]
description: "Jenkins - Vulnerabilities analysis part 3"
---

## Summary
What's coming from all the precedent numbers are this list of vulnerabilities by category. This is interresting to see what kind of bug can be found on Jenkins.

## Numbers
- 37 - Missing permission
- 36 - XSS
- 29 - CSRF
- 11 - XXE
- 11 - Secret stored in plain text
- 7 - Path traversal
- 6 - Agent-to-controller security bypass
- 3 - Arbitrary file read
- 3 - Denial of service
- 3 - Incorrect permission
- 3 - Sandbox bypass vulnerability
- 2 - Open redirect
- 2 - OS command execution
- 2 - SSL/TLS
- 2 - RCE
- 2 - Bypassing CSRF protection
- 1 - Agent-to-controller access control allowed writing to sensitive directory
- 1 - Agent-to-controller access control allows reading/writing most content of build directories
- 1 - Arbitrary file existence check
- 1 - Arbitrary file write
- 1 - Arbitrary JSON and property file read
- 1 - Bypassing path filtering
- 1 - Improper credentials masking
- 1 - Improper handling of equivalent directory names
- 1 - Improper handling of REST API XML deserialization errors
- 1 - Improper permission
- 1 - Lack of type validation
- 1 - Missing synchronization 
- 1 - Non-constant time token comparison
- 1 - Password parameter default values exposed
- 1 - Privilege escalation
- 1 - Sensitive information disclosure
- 1 - Sensitive parameter values captured in build metadata files
- 1 - Session fixation
- 1 - Support bundles can include user session IDs
- 1 - User passwords transmitted in plain text
- 1 - View name validation bypass

## Calculus
Which makes a total of **180** vulnerabilities in about 15 month. This can be view as **12** vulnerabilities found by month.

Top 10 vulnerability found in 15 month :
1. Missing permission
2. XSS
3. CSRF
4. XXE
5. Secret stored in plain text
6. Path traversal
7. Agent-to-controller security bypass
8. Arbitrary file read
9. Denial of service
10. Incorrect permission


Which is a total of **146** vulnerabilities or **81,1%** of the total during this period.
1. Missing permission --> 20,5%
2. XSS --> 20%
3. CSRF --> 16,1%
4. XXE --> 6,1%
5. Secret stored in plain text --> 6,1% 
6. Path traversal --> 3,8%
7. Agent-to-controller security bypass --> 3,3%
8. Arbitrary file read --> 1,6%
9. Denial of service --> 1,6%
10. Incorrect permission --> 1,6%

## What's next ?
Next part of this analysis, will be about making a lab to study some of the vulnerabilities from my top 10. This will be a docker image containing vulnerable plugins and there will be a "write up" on how to trigger them.

See [Jenkins - Vulnerability analysis part 4](https://liodeus.github.io/2022/03/20/Jenkins-Vulnerabilities-analysis-part-4.html).
