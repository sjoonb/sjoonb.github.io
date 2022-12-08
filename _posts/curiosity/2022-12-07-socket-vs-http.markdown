---
layout: post
title:  "Difference between socket programming and HTTP programming"
categories: curiosity
date:  2022-12-07 23:21:22 +0900
---

<br/>
**HTTP Connection**

- HTTP connection is a protocol that runs on a socket.
- HTTP connection is a higher-level abstraction of a network connection.
- With HTTP connection the implementation takes care of all these higher-level details and simply send HTTP request (some header information) and receive HTTP response from the server.

**Socket Connection**

- Socket is used to transport data between systems. It simply connects two systems together, an IP address is the address of the machine over an IP based network.
- With socket connection you can design your own protocol for network connection between two systems.
- With Socket connection you need to take care of all the lower-level details of a TCP/IP connection.

`HTTP` is an application protocol. It basically means that HTTP itself can't be used to transport information to/from a remote end point. Instead it relies on an underlying protocol which in HTTP's case is `TCP`.

`Sockets` on the other hand are an API that most operating systems provide to be able to talk with the network. The socket API supports different protocols from the transport layer and down.

That means that if you would like to use TCP, you have to use sockets. But you can also use sockets to communicate using HTTP, but then you have to decode/encode messages according to the HTTP specification (RFC2616). Since that can be a huge task for most developers we also got ready clients in our developer frameworks (like .NET), for instance the WebClient or the HttpWebRequest classes.





<br/>
## References

- [https://stackoverflow.com/questions/15108139/difference-between-socket-programming-and-http-programming](https://stackoverflow.com/questions/15108139/difference-between-socket-programming-and-http-programming)