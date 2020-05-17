---
layout: page
title: Link Layer and LANs
tags: Computer_Network
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<!--more-->

## Link Layer and LANs

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