---
layout: post
title:  "Prerequisite knowledge"
categories: tetris
date:  2022-12-06 11:26:31 +0900
---


- [network socket](#network-socket)
- [Internet protocol suite](#internet-protocol-suite)
  - [Key architectural principles](#key-architectural-principles)
- [transport protocol](#transport-protocol)


<br/>
### network socket

A `network socket` is a **software structure** within a network node of a  computer network that serves as an endpoint for sending and receiving data across the network. The structure and properties of a socket are defined by an API for the networking architecture. Sockets are created only during the lifetime of a process of an application running in the node.

Because of the standardization of the `TCP/IP` protocols in the development of the Internet, the term network socket is most commonly used in the context of the [**Internet protocol suite**](#internet-protocol-suite), and is therefore often also referred to as **Internet socket**. In this context, a socket is externally identified to other hosts by its `socket address`, which is the triad of [**transport protocol**](#transport-protocol), **IP address**, and **port number**. 


<br/>
### Internet protocol suite

The Internet protocol suite, commonly known as TCP/IP, is a **framework for organizing the set of communication protocols** used in the Internet and similar computer networks according to functional criteria. The foundational protocols in the suite are the `Transmission Control Protocol (TCP)`, the `User Datagram Protocol (UDP)`, and the `Internet Protocol (IP)`

The Internet protocol suite provides end-to-end data communication specifying **how data should be packetized, addressed, transmitted, routed, and received**. 

#### Key architectural principles

<br/>
### transport protocol

In computer networking, the transport layer is a conceptual division of methods in the layered architecture of  protocols in the network stack in the Internet protocol suite and 





<br/>
<br/>
참고
- [https://en.wikipedia.org/wiki/Network_socket](https://en.wikipedia.org/wiki/Network_socket)
- [https://en.wikipedia.org/wiki/Internet_protocol_suite](https://en.wikipedia.org/wiki/Internet_protocol_suite)
- [https://en.wikipedia.org/wiki/Transport_layer](https://en.wikipedia.org/wiki/Transport_layer)