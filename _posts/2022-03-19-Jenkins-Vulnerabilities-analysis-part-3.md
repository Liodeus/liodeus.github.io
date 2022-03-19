---
layout: post
title: Jenkins - Vulnerabilities analysis part 3
tags: [Jenkins, Security, CI, CD]
description: "Jenkins - Vulnerabilities analysis part 3"
---

## Summary
What's coming from all the precedent numbers are this list of vulnerabilities by category. This is interresting to see what kind of bug can be found on Jenkins.

## Numbers
- 38 - Missing permission
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
Which makes a total of **181** vulnerabilities in about 15 month.

TO FINISH (make percentages)