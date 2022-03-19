---
layout: post
title: Jenkins - Vulnerabilities analysis part 2
tags: [Jenkins, Security, CI, CD]
description: "Jenkins - Vulnerabilities analysis part 2"
---

This is the second part of my post about Jenkins security. So after getting all the vulnerabilities name, I sorted them by vulnerability "categorie" and write their numbers like so : **Vuln_name - Number_This_Month**

## January - 2021
- Path traversal - 1
- Arbitrary file existence check - 1
- Denial of service - 1
- Missing permission - 1
- Improper handling of REST API XML deserialization errors - 1
- Arbitrary file read - 2
- Credentials stored in plain text - 2
- XSS - 4
- 
## February - 2021
- Support bundles can include user session IDs - 1
- Privilege escalation - 1
- CSRF - 2
- XSS - 4
- 
## March - 2021
- Passwords stored in plain text - 1
- Incorrect permission - 2
- XSS - 3
- CSRF - 4
- Missing permission - 6

## April - 2021
- Incorrect permission - 1
- RCE - 1
- XSS - 1
- XXE - 1
- DOS - 1
- Lack of type validation - 1
- View name validation bypass - 1
- SSL/TLS - 1
- Missing permission - 3
- CSRF - 3

## May - 2021
- CSRF - 2
- XSS - 3
- Missing permission - 4
- XXE - 4

## June - 2021
- Improper permission - 1
- Session fixation - 1
- Open redirect - 1
- CSRF - 2
- XXE - 2
- XSS - 3
- Missing permission - 5

## August - 2021
- RCE - 1
- XXE - 1
- Password stored in plain text - 1
- Bypassing CSRF protection - 2

## October - 2021
- Path traversal - 1
- SSL/TLS - 1
- XSS - 1
- Improper handling of equivalent directory names - 1

## November - 2021
- Bypassing path filtering - 1
- Arbitrary file write - 1
- Path traversal - 1
- Agent-to-controller access control allowed writing to sensitive directory - 1
- Agent-to-controller access control allows reading/writing most content of build directories - 1
- XSS - 2
- XXE - 3

## January 2022
- Password stored in plain text - 1
- Access key stored in plain text - 1
- OS command execution - 1
- Improper credentials masking - 1
- Non-constant time token comparison - 1
- User passwords transmitted in plain text - 1
- Path traversal - 2
- Agent-to-controller security bypass - 3
- XSS - 3
- CSRF - 5
- Missing permission - 5

## February
- Open redirect - 1
- DOS - 1
- OS command execution - 1 - 
- Sensitive data stored in plain text - 1
- Missing synchronization  - 1
- Password parameter default values exposed - 1
- Sensitive information disclosure - 1
- Arbitrary file read - 1
- Path traversal - 2
- Agent-to-controller security bypass - 2
- Sandbox bypass vulnerability - 3
- XSS - 5
- CSRF - 7
- Missing permission - 8

## March - 2022
- Sensitive parameter values captured in build metadata files - 1
- Client Secret stored in plain text - 1
- Arbitrary JSON and property file read - 1
- Arbitrary file read - 1
- Personal tokens stored in plain text - 1
- Agent-to-controller security bypass - 1
- Passwords stored in plain text - 2
- CSRF - 4
- Missing permission - 5
- XSS - 7

Next part of this analysis, will be about adding numbers. To find out if there is some vulnerability which are more recurent than others, see [Jenkins - Vulnerability analysis part 3](https://liodeus.github.io/2022/03/19/Jenkins-vulnerabilities-analysis-part-3.html).