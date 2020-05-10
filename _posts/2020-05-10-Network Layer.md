---
layout: page
title: Computer Network
tags: Computer Network
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<!--more-->

_index_

- introduction
- Virtual circuit and datagram networks
- What’s inside a router 
- IP
- Routing algorithms 
- Routing in the Internet
- Broadcast and multicast routing

## introduction

- Forwarding and Routing
- Connection setup

### network service model

|    example services for individual datagrams     |    example services for a flow of datagrams     |
| :----------------------------------------------: | :---------------------------------------------: |
|               guaranteed delivery                |           in-order datagram delivery            |
| guaranteed delivery with less than 40 msec delay |      guaranteed minimum bandwidth to flow       |
|                                                  | restrictions on changes in inter-packet spacing |

## Virtual circuit and datagram network

- datagram network provides network-layer **connectionless** service
- VC network provides network-layer **connection** service

### Virtual circuits

Virtual circuits works like telephone circuits

- each packet carries VC identifier
- Every router on source-dest path maintains “state” for each passing connection

### Datagram networks

- no call setup at network layer
- Routers: no state about end-to-end connections 
- Packets forwarded using destination host address

**Longest prefix matching**

[VC and datagram network](https://blog.csdn.net/qq_22238021/article/details/80426135)

## IP: Internet Protocol

_index_

- Datagram
- IPv4 addressing
- ICMP
- IPv6

### Datagram

_IP datagram format_

![](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcQV2DGaDItOTPoZrjQPlnz0Sqy2gsc_2ns07me8kOPLKtGyZhXN_KuDw-yQ)

_IP Fragmentation & Reassembly_

Network links have MTU(max transfer size)

When sum length L>MTU, it needs fragmentation.
[Fragmentation & Reassembly](https://www.cnblogs.com/sqmlinux/archive/2012/12/04/2801643.html)

### IPv4 addressing

**IP address:**

- subnet part(higher order bits)
- Host part(low order bits)

**IP addressing: CIDR**

a.b.c.d/x
x is the number of bits in subnet portion of address 

**IP address: how to get one ?**

**DHCP:**using UDP

1. Host broadcasts “DHCP discover” msg
2. DHCP server responds with “DHCP offer” msg
3. Host requests IP address “DHCP request” msg
4. DHCP server sends address “DHCP ack” msg

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/DHCP_session.svg/260px-DHCP_session.svg.png)


## Routing algorithm

Dynamic:

- LS: Link State(OSPF)
- DV: Distance vector(RIP)

LS:

- Global
- Dijkstra algorithm

DV:

- decentralized 

### Hierarchical routing

AS: autonomous system

Routers in the same AS run the same routing rule

## Routing in the Internet

### RIP: DV 

- At most 15 hops
- Based on hop
- used in small-scale network
- Update every 30s, over 180s no response(unreachable), over 240s(delete)
- use UDP
- routing table managed by application layer route-daemon

### OSPF: LS

- based on bandwidth 
- Carry OSPF msgs over IP(instead of UDP/TCP)
- Hierarchical OSPF

### BGP(border gateway protocol)

- used between ASs

- EBGP: between different ASs
- IBGP: among the same AS to prevent circuit