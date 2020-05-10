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