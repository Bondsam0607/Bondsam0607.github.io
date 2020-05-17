---
layout: page
title: Computer Network
tags: Computer_Network
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<!--more-->

_index_

- Application architecture
- HTTP&Web
- electronic mail
- DNS
- P2P
- CDNs

## Application architecture

- C/S architecture（client-server）
- peer-to-peer（p2p）
- use socket
- Internet transmission protocol
  - TCP
  - UDP

## HTTP&Web

_index_

- HTTP overview
- Non-persistent&persistent
- Updating form input
- Cookie
- Web cache
- Conditional GET

____________________________________

**‌HTTP is a application protocol**

### HTTP overview：

- use TCP
- HTTP is ‘stateless’
  - server maintains no info about past client requests

### non-persistent&persistent：

|                     non-persistent HTTP                      |                       persistent HTTP                        |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|           multiple objects required multiple TCPs            |         multiple objects can be sent over single TCP         |
|                  requires 2 RTTs per object                  |     server leaves connection open after sending response     |
|             OS overhead for each TCP connection              | subsequent HTTP messages between same client/server sent over open connection |
| browsers often parallel TCP connections to fetch referenced objects | client sends requests as soon as it encounters a referenced object |
|                                                              |     as little as one RTT for all the referenced objects      |

### Uploading form input

|                POST method                 |                   URL method                   |
| :----------------------------------------: | :--------------------------------------------: |
|     web page often includes form input     |                uses GET method                 |
| input is uploaded to server in entity body | input is uploaded in URL field of request line |

### Cookies

**keeping “state” use ID**

four components:

- cookie header line of HTTP response message
- cookie header line in next HTTP request message
- cookie file kept on user’s host, managed by user’s browser
- back-end database at Web site

### Web caches(proxy server)

**satisfy client without involving origin server**

- Store objects in cache
- Browser sends all HTTP requests to cache
  - object in cache:cache returns object
  - else cache requests object from origin server, then returns object to client

____________________________________

1. cache acts as both client and server
2. typically cache is installed by ISP


### Conditional GET

**don’t send object if cache has up-to-date cached version**

## electronic mail

_index_

- SMTP
- POP3
- IMAP

________________________________________________________________

### SMTP:final words

- SMTP uses persistent connections
- SMTP requires message to be in 7-bit ASCII
- SMTP server uses CRLF.CRLF to end the message

### POP3

- “download-and-delete mode”: cannot re-read e-mail if the client is changed
- “download-and-keep”: copies of messages on different clients
- POP3 is stateless across sessions

### IMAP

- keeps all msgs in one place: at server
- Allows user to organize msgs in folders
- Keeps user state across sessions: names of folders and mappings between messages IDs and folder name

## DNS: domain name system

- distributed database
- Application-layer protocol

____________________________________

- root name servers
- Top-level domain servers(com,cn...)
- Authoritative DNS servers
- Local DNS name servers

____________________________________

DNS records

- type=A _ip directing_
- type=NS _name server_
- type=CNAME _alias directing_
- type=MX _mail exchange_

## P2P applications

|                       client-server                        |                             P2P                              |
| :--------------------------------------------------------: | :----------------------------------------------------------: |
| D<sub>c-s</sub> >= max{NF/u<sub>s</sub>,F/d<sub>min</sub>} | D<sub>P2P</sub> >= max{F/u<sub>s</sub>,F/d<sub>min</sub>,NF/(u<sub>s</sub> + Σu<sub>i</sub>)} |

### P2P file distribution: BitTorrent

BitTorrent:

- tracker: tracks peers participating in torrent
- torrent: group of peers exchanging chunks of a file

## video streaming and content distribution networks(CDNs)



# Transport Layer

_index_

- transport-layer services
- Multiplexing and demultiplexing
- Connectionless transport: UDP
- Principles of reliable data transfer(rdt)
- Connection-oriented transport: TCP
- Principle of congestion control
- TCP congestion control

## transport-layer services

- Transport-layer is used to provide logical communication between apps. 
- It breaks msgs into several segments in the sender side and reunite them in order in the receiver side. 
- Use TCP and UDP

## Multiplexing and Demultiplexing

Multiplexing at sender:
Handle data from multiple sockets, add transport header

Demultiplexing at receiver:
Use header info to deliver segments to correct socket. Use IP addresses and port numbers.

|                     Connectionless demux                     |                  Connection-oriented demux                   |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|                             UDP                              |                             TCP                              |
| datagram with same IP addr and source port will be directed into to same socket | datagram with same IP addr and source port but from different source IP will be directed to different sockets |

## Connectionless transport: UDP

### UDP overview

_connectionless:_

- no handshaking
- each UDP segment handle independently of each other

> to ensure reliable data transfer upon UDP:
>
> - add reliability at application-layer
> - application-specific error recovery

Merits of UDP:

- no connection establishment(less delay)
- Simple: no connection state at sender, receiver
- Smaller header size
- No congestion control

### UDP: segment header

8 bytes: 64 bits

- Source port
- dest port
- Length
- Checksum

#### Checksum

Add the source port and dest port, if there’s a carry out from the most significant bit, it needs to be added to least significant bit of the result.

Then add the result and the length, do a bit conversion and get the checksum.

## principle of reliable data transfer

- rdt1.0:reliable transfer over a reliable channel

- rdt2.0: channel with bit errors 
  - error detection
  - ACK&NAK
  - Retransmission

- rdt2.1: with 0,1 
  - figure out the bit error problem of ACK and NAK

> for example, the receiver is waiting for ‘0’ packet, but get ‘1’ packet, it will send ACK1. This time, the sender is waiting for ACK0, when it get ACK1, it will resend ‘0’ packet.

- rdt2.2: drop NAK
  - use ACK only
  - Duplicated ACK = NAK

- rdt3.0: channel with errors and loss
  - package loss
  - Timer
  - Pipeline———GBN
  - SR

## connection-oriented transport: TCP

### segment structure

- header: 20bytes
- sequence numbers:
  - byte stream number of first byte in segment’s data
- acknowledgements:
  - seq of next byte expected from the other side
  - Cumulative ACK

![](https://i0-wp-com.cdn.ampproject.org/ii/w1200/s/i0.wp.com/madpackets.com/wp-content/uploads/2018/04/tcp-seq-ack-flow-e1524681839913.png?resize=538%2C756&ssl=1)


- TCP timeout

  - should be longer than RTT

  > how to estimate RTT
  >
  > > SampleRTT:measured time from segment transmission until ACK receipt
  > >
  > > EstimatedRTT = (1-a)EstimatedRTT + a * SampleRTT
  > >
  > > **typically value: a=0.125**

  > timeout interval
  >
  > > estimate SampleRTT deviation from EstimatedRTT:
  > >
  > > DevRTT = (1-b)*DevRTT + b*|SampleRTT-EstimatedRTT|
  > >
  > > **typically,b=0.25**
  > >
  > > TimeoutInterval = EstimatedRTT + 4*DevRTT(safety margin)

### TCP rdt

Retransmission triggered by:

- timeout events
- Duplicate acts

TCP fast retransmit(don’t wait for timeout)
If sender receives 3 ACKs for same data, resend unasked segment with smallest seq.

### flow control

[see the blog](https://blog.csdn.net/Bondsam/article/details/89461546)

### connection management

3-way handshake

Closing a connection: TCP segment sending FIN bit = 1

## principles of congestion control

[congestion control](https://blog.csdn.net/metasearch/article/details/8205795)



# Network Layer

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




### Link Layer and LANs

**Terminology:**

- Nodes
- Links
- Frame

_data-link layer has responsibility of transferring datagram to adjacent nodes_

Link layer is implemented in NIC(network interface card)

|:-:|:-:|
|**sending side**|**receiving side**|
|encapsulate|looks for error,flow control|
|add error checking bits,flow controk|extract|

## error detection, correction

EDC: error detection and correction bits

D: data

Not 100% reliable