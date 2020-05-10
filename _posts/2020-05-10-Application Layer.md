---
layout: page
title: Application Layer
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