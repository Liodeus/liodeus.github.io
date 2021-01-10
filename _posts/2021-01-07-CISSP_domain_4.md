---
layout: post
title: 
tags: []
description: ""
---

# Communication and Network Security

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

![TCP/IP Model: Layers & Protocol | What is TCP IP Stack?](https://www.guru99.com/images/1/093019_0615_TCPIPModelW3.png)

