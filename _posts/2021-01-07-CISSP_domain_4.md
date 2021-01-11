---
layout: post
title: Communication and Network Security - CISSP
tags: [CISSP, CHAPTER_4, Communication and Network Security]
description: "Communication and Network Security - Chapter 4"
---

# Communication and Network Security

## OSI model - TCP/IP

| Layers  | OSI          | TCP/IP            |
| ------- | ------------ | ----------------- |
| Layer 7 | Application  | Application       |
| Layer 6 | Presentation | Application       |
| Layer 5 | Session      | Application       |
| Layer 4 | Transport    | Transport         |
| Layer 3 | Network      | Network           |
| Layer 2 | Data Link    | Network Interface |
| Layer 1 | Physical     | Network Interface |

Mnemonics : **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

### Application

Handle file transfer, virtual terminals, network management, and fulfilling networking requests of applications. 

- FTP
- SNMP
- SMTP
- Telnet
- HTTP

### Presentation

Handle translation into standard formats, data compression/decompression, and data encryption/decryption. No protocols work at
this layer, just services.

- ASCII
- JPEG
- MIDI

### Session

Set up connections between applications; maintain dialog control; and negotiate, establish, maintain, and tear down the communication channel.

- NetBIOS
- PPTP (Point-to-Point Tunneling Protocol)
- RPC

### Transport

Handle end-to-end transmission and segmentation of a data stream.

- TCP
- UDP

### Network

The responsibilities of the network layer protocols include internetworking service, addressing, and routing.

- IP
- ICMP
- IPX (Internetwork Packet Exchange )

### Data Link

Convert data into LAN or WAN frames for transmission and define how a computer accesses a network. This layer is divided into the Logical Link Control (LLC) and the Media Access Control (MAC) sublayers.

- ARP
- PPP (Point-to-Point Protocol)
- Ethernet (IEEE 802.3)
- Token Ring (IEEE 802.5)

### Physical

Network interface cards and drivers convert bits into electrical signals and control the physical aspects of data transmission, including optical, electrical, and mechanical requirements.

- 10Base-T, 10Base2, 10Base5, 100Base-TX, 100Base-FX, 100Base-T, 1000Base-T, 1000Base-SX
- DSL

![](/assets/imgs/CISSP/CH04/osi_tcp_model.png)

Encapsulation : refer to a process in which protocol information is added to the data when it passes through the layers. Protocol information can be added before (header) and after the data (trailer). 

![](/assets/imgs/CISSP/CH04/one.PNG)

Simplex : Communication takes place in one direction.

Half-Duplex : Communication takes place in both directions, but only one application can send information at a time.

Full-Duplex : Communication takes place in both directions, and both applications can send information at the same time.















## Dual stacks

Dual stacks enable a host to communicate with both IPv4 hosts and IPv6 hosts. Dual stack devices are configured with an IPv4 address and an IPv6 address; thus, a dual stack device can communicate directly with both IPv4 and IPv6 devices withou requiring protocol translation.

## IPv4 to IPv6 only

4to6 tunneling : encapsulates an IPv4 packet inside an IPv6 header.

## IPv6 to IPv4 only

6to4 tunneling : encapsulates an IPv6 packet inside an IPv4 header.

## Network Address Translation-Protocol Translation (NAT-PT)

Enables and IPv4-only host to communicate with an IPv6-only host and enables an IPv6-only host to communicate with an IPv4-only host. NAT-PT translates IPv4 packets to IPv6 packets and translates IPv6 packets to IPv4 packets. Router must contain address mappings to correctly translate IPv4 and IPv6.

## Multiple broadcast domains

Broadcast packets from one broadcast domain are not forwarded to other broadcast domains. In a router, each routed network interface creates a separate broadcast domain. You can also create a virtual local area network (VLAN) on a Layer 3 switch to create a separate broadcast domain. Each VLAN creates a separate broadcast domain.

![https://cdn.networklessons.com/wp-content/uploads/2016/11/xrouter-breaks-broadcast-domain.png.pagespeed.ic.FzR4ox_5t4.png](https://cdn.networklessons.com/wp-content/uploads/2016/11/xrouter-breaks-broadcast-domain.png.pagespeed.ic.FzR4ox_5t4.png)

We have three broadcast domains, one on each side of the router.



