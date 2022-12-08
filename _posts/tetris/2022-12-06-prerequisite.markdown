---
layout: post
title:  "Prerequisite knowledge"
categories: tetris
date:  2022-12-06 11:26:31 +0900
---


- [network socket](#network-socket)
    - [use](#use)
    - [Socket addresses](#socket-addresses)
    - [Iplementation](#iplementation)
    - [Example](#example)
    - [Types](#types)
    - [Socket states in the client-server model](#socket-states-in-the-client-server-model)
    - [Socket pairs](#socket-pairs)
- [Internet protocol suite](#internet-protocol-suite)
    - [Key architectural principles](#key-architectural-principles)
- [IP address](#ip-address)
- [Port number](#port-number)
- [transport protocol](#transport-protocol)
- [file descriptor](#file-descriptor)
    - [Overview](#overview)
- [References](#references)



<br/>
## network socket

A `network socket` is a **software structure** within a network node of a  computer network that serves as an endpoint for sending and receiving data across the network. The structure and properties of a socket are defined by an API for the networking architecture. Sockets are created only during the lifetime of a **process** of an application running in the node.

Because of the standardization of the `TCP/IP` protocols in the development of the Internet, the term network socket is most commonly used in the context of the [Internet protocol suite](#internet-protocol-suite), and is therefore often also referred to as **Internet socket**. In this context, a socket is externally identified to other hosts by its `socket address`, which is the triad of [transport protocol](#transport-protocol), [IP address](#ip-address), and **port number**. 

<br/>
#### use

The API for the network protocol stack creates a handle for each socket created by an applictaion, commonly referred to as a socket descriptor. In Unix-like operating systems, this descriptor is a type of [file descriptor](#file-descriptor). It is stored by the application process for use with every read and write operation on the communication channel.


At the time of creation with the API, a network socket is bound to the combination of a type of network protocol to be used for transmissions, a network address of the host, and a port number. `Ports` are numbered resources that represent another type of software structure of the node. They are used as service types, and, once created by a process, serve as an externally (from the network) addressable location component, so that other hosts may establish connections.

Network sockets may be dedicated for persistent connections for communication between two nodes, or they may participate in connectionless and multicast communications.

In practice, due to the proliferation of the `TCP/IP` protocols in use on the Internet, the term network socket usually refers to use with the `Internet Protocol (IP)`. It is therefore often also called **Internet socket**.

<br/>
#### Socket addresses

An application can communicate with a remote process by exchanging data with TCP/IP by knowing the combination of protocol type, IP address, and port number. This combination is often known as a **socket address**. It is the network-facing access handle to the network socket. The remote process establishes a network socket in its own instance of the protocol stack, and uses the networking API to connect to the application, presenting its own socket address for use by the application.


<br/>
#### Iplementation

A `protocol stack`, usually provided by the `operating system`, is a set of services that allow processes to communicate over a network using the protocols that the stack implements. The operating system forwards the payload of incoming IP packets to the corresponding application by extracting the socket address information from the IP and transport protocol headers and stripping the headers from the application data.

The application programming interface (API) that programs use to communicate with the protocol stack, using network sockets, is called a **socket API**. Development of application programs that utilize this API is called `socket programming` or network programming. Internet socket APIs are usually based on the Berkeley sockets standard. In the Berkeley sockets standard, sockets are a form of [file descriptor](#file-descriptor), due to the Unix philosophy that "everything is a file", and the analogies between sockets and files. Both have functions to read, write, open, and close. In practice the differences strain the analogy, and different interfaces (send and receive) are used on a socket.

In the standard Internet protocols `TCP` and `UDP`, a socket address is the combination of an [IP address](#ip-address) and a [port number](#port-number). Sockets need not have a source address, for example, for only sending data, but if a program binds a socket to a source address, the socket can be used to receive data sent to that address. Based on this address, Internet sockets deliver incoming data packets to the appropriate application process.

<br/>
#### Example

This example, modeled according to the Berkeley socket interface, sends the string "Hello, world!" via TCP to port 80 of the host with address 1.2.3.4. It illustrates the creation of a socket (getSocket), connecting it to the remote host, sending the string, and finally closing the socket:

```
Socket mysocket = getSocket(type = "TCP")
connect(mysocket, address = "1.2.3.4", port = "80")
send(mysocket, "Hello, world!")
close(mysocket)
```

<br/>
#### Types

**Datagram sockets**

Connectionless sockets, which use `User Datagram Protocol (UDP)`. Each packet sent or received on a datagram socket is individually addressed and routed. Order and reliability are not guaranteed with datagram sockets, so multiple packets sent from one machine or process to another may arrive in any order or might not arrive at all. Special configuration may be required to send broadcasts on a datagram socket. In order to receive broadcast packets, a datagram socket should not be bound to a specific address, though in some implementations, broadcast packets may also be received when a datagram socket is bound to a specific address.


**Stream sockets**

Connection-oriented sockets, which use `Transmission Control Protocol (TCP)`, Stream Control Transmission Protocol (SCTP) or Datagram Congestion Control Protocol (DCCP). A **stream socket** provides a sequenced and unique flow of **error-free data** without record boundaries, with well-defined mechanisms for creating and destroying connections and reporting errors. A stream socket transmits data **reliably**, **in order,** and with out-of-band capabilities. On the Internet, stream sockets are typically implemented using TCP so that applications can run across any networks using TCP/IP protocol.

<br/>
#### Socket states in the client-server model

Computer processes that provide application services are referred to as **servers**, and create sockets on startup that are in the *listening state*. These sockets are waiting for initiatives from **client** programs.

A `TCP server` may serve several clients concurrently by creating a unique dedicated socket for each client connection in a new child process or processing thread for each client. These are in the established state when a socket-to-socket virtual connection or virtual circuit (VC), also known as a TCP session, is established with the remote socket, providing a duplex **byte stream**.

A server may create several concurrently established `TCP sockets` with the **same local port number and local IP address**, each mapped to its own **server-child process**, serving its own client process. They are treated as **different sockets** by the operating system since the remote socket address (the client IP address or port number) is different; i.e. since they have different socket pair tuples.

`UDP sockets` do not have an established state, because the protocol is connectionless. A UDP server process handles incoming datagrams from all remote clients sequentially through the **same socket**. UDP sockets are not identified by the remote address, but only by the local address, although each message has an associated remote address that can be retrieved from each datagram with the networking application programming interface (API).

<br/>
#### Socket pairs
Communicating local and remote sockets are called socket pairs. Each socket pair is described by a unique 4-tuple consisting of **source** and **destination** **IP addresses** and **port numbers**, i.e. of local and remote socket addresses. As discussed above, in the TCP case, a socket pair is associated on each end of the connection with a unique 4-tuple.


<br/>
<br/>
## Internet protocol suite

The Internet protocol suite, commonly known as TCP/IP, is a **framework for organizing the set of communication protocols** used in the Internet and similar computer networks according to functional criteria. The foundational protocols in the suite are the `Transmission Control Protocol (TCP)`, the `User Datagram Protocol (UDP)`, and the `Internet Protocol (IP)`

The Internet protocol suite provides end-to-end data communication specifying **how data should be packetized, addressed, transmitted, routed, and received**. 

<br/>
#### Key architectural principles

<br/>
![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c4/IP_stack_connections.svg/700px-IP_stack_connections.svg.png)
*Conceptual data flow in a simple network topology of two hosts (<i>A</i> and <i>B</i>) connected by a link between their respective routers. The application on each host executes read and write operations as if the processes were directly connected to each other by some kind of data pipe. After establishment of this pipe, most details of the communication are hidden from each process, as the underlying principles of communication are implemented in the lower protocol layers. In analogy, at the transport layer the communication appears as host-to-host, without knowledge of the application data structures and the connecting routers, while at the internetworking layer, individual network boundaries are traversed at each router.*


<br/>
![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3b/UDP_encapsulation.svg/700px-UDP_encapsulation.svg.png)
*Encapsulation of application data descending through the layers described in RFC 1122*

<br/>
The **end-to-end principle** has evolved over time. Its original expression put the maintenance of state and overall intelligence at the edges, and assumed the Internet that connected the edges retained no state and concentrated on speed and simplicity. Real-world needs for firewalls, network address translators, web content caches and the like have forced changes in this principle.

The **robustness principle** states: "In general, an implementation must be conservative in its sending behavior, and liberal in its receiving behavior. That is, it must be careful to send well-formed datagrams, but must accept any datagram that it can interpret (e.g., not object to technical errors where the meaning is still clear)." "The second part of the principle is almost as important: software on other hosts may contain deficiencies that make it unwise to exploit legal but obscure protocol features."

**Encapsulation** is used to provide abstraction of protocols and services. Encapsulation is usually aligned with the division of the protocol suite into layers of general functionality. In general, an application (the highest level of the model) uses a set of protocols to **send its data down the layers**. The data is further encapsulated at each level.

- The `application layer` is the scope within which **applications**, or **processes**, create user data and communicate this data to **other applications** on another or the same host. The applications make use of the services provided by the underlying lower layers, especially the `transport layer` which provides **reliable or unreliable pipes to other processes**. The communications partners are characterized by the application architecture, such as the **client–server model** and **peer-to-peer** networking. This is the layer in which all application protocols, such as `SMTP`, `FTP`, `SSH`, `HTTP`, operate. Processes are addressed via ports which essentially represent services.

- The `transport layer` performs **host-to-host** communications on either the local network or remote networks separated by routers. It provides a channel for the communication needs of applications. `UDP` is the basic transport layer protocol, providing an **unreliable connectionless** datagram service. The `TCP` provides flow-control, connection establishment, and **reliable transmission** of data.

- The `internet layer` exchanges datagrams across network boundaries. It provides a uniform networking interface that hides the actual topology (layout) of the underlying network connections. It is therefore also the layer that establishes internetworking. Indeed, it defines and establishes the Internet. This layer defines the **addressing and routing structures** used for the `TCP/IP` protocol suite. The primary protocol in this scope is the Internet Protocol, which defines `IP` addresses. Its function in routing is to transport datagrams to the next host, functioning as an IP router, that has the connectivity to a network closer to the final data destination.

- The `link layer` defines the networking methods within the scope of the local network link on which hosts communicate without intervening routers. This layer includes the protocols used to describe the local network topology and the interfaces needed to affect the transmission of Internet layer datagrams to next-neighbor hosts.


<br/>
<br/>
## IP address

An Internet Protocol address (**IP address**) is a numerical label such as 192.0.2.1 that is connected to a computer network that uses the Internet Protocol for communication. An IP address serves two main functions: **network interface identification** and **location addressing**.

**Internet Protocol version 4** (IPv4) defines an IP address as a 32-bit number. However, because of the growth of the Internet and the depletion of available IPv4 addresses, a new version of IP (**IPv6**), using 128 bits for the IP address, was standardized in 1998


[learn more about IP address]({% post_url 2022-12-07-internet-protocol %})


<br/>
<br/>
## Port number

In **computer networking**, a port is a number assigned to uniquely identify a connection endpoint and to direct data to a specific service. At the software level, within an **operating system**, a port is a logical construct that identifies a specific **process** or a type of **network service**. A port is identified for each [transport protocol](#transport-protocol) and address combination by a **16-bit unsigned number**, known as the port number. The most common transport protocols that use port numbers are the `Transmission Control Protocol (TCP)` and the `User Datagram Protocol (UDP)`.

A `port number` is always associated with an [IP address](#ip-address) of a host and the type of [transport protocol](#transport-protocol) used for communication. It completes the destination or origination network address of a message. Specific port numbers are reserved to identify specific services so that an arriving packet can be easily forwarded to a running application. For this purpose, port numbers lower than 1024 identify the historically most commonly used services and are called the [well-known port](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers#Well-known_ports) numbers. Higher-numbered ports are available for general use by applications and are known as ephemeral ports.

<br/>
<br/>
## transport protocol

In computer networking, the transport layer is a conceptual division of methods in the layered architecture of  protocols in the network stack in the [Internet protocol suite](#internet-protocol-suite) and the OIS model. The protocols of this layer provide **end-to-end** communication services for applications. It provides services such as **connection-oriented communication, reliability, flow control, and multiplexing**.

The best-known transport protocol of the Internet protocol suite is the `Transmission Control Protocol (TCP)`. It is used for **connection-oriented transmissions**, whereas the **connectionless** `User Datagram Protocol (UDP)` is used for simpler messaging transmissions. TCP is the more complex protocol, due to its stateful design incorporating reliable transmission and data stream services. Together, TCP and UDP comprise essentially all traffic on the Internet and are the only protocols implemented in every major operating system. 



<br/>
<br/>
## file descriptor

In Unix and Unix-like computer operating systems, a file descriptor (FD, less frequently fildes) is a **process-unique identifier** (handle) for a **file** or other input/output resource, such as a **pipe** or **network socket**.


<br/>
#### Overview

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f8/File_table_and_inode_table.svg/600px-File_table_and_inode_table.svg.png)
*File descriptors for a single process, file table and inode table. Note that multiple file descriptors can refer to the same file table entry and that multiple file table entries can in turn refer to the same inode (if it has been opened multiple times; the table is still simplified because it represents inodes by file names, even though an inode can have multiple names). File descriptor 3 does not refer to anything in the file table, signifying that it has been closed.*

In the traditional implementation of Unix, file descriptors index into a per-process **file descriptor table** maintained by the kernel, that in turn indexes into a system-wide table of files opened by all processes, called the **file table**. This table records the mode with which the file (or other resource) has been opened: for reading, writing, appending, and possibly other modes. It also indexes into a third table called the **inode table** that describes the actual underlying files. To perform input or output, the process passes the file descriptor to the kernel through a `system call`, and the kernel will access the file on behalf of the process. The process does not have direct access to the file or inode tables.

On `Linux`, the set of file descriptors open in a process can be accessed under the path /proc/PID/fd/, where **PID** is the process identifier. File descriptor /proc/PID/fd/0 is **stdin**, /proc/PID/fd/1 is **stdout**, and /proc/PID/fd/2 is **stderr**. As a shortcut to these, any running process can also access its own file descriptors through the folders /proc/self/fd and /dev/fd.

In Unix-like systems, file descriptors can refer to any Unix file type named in a file system. As well as **regular files**, this includes **directories**, block and character devices (also called "special files"), Unix domain sockets, and named pipes. File descriptors can also refer to other objects that do not normally exist in the file system, such as anonymous pipes and **network sockets**.

[learn more about file descriptor]({% post_url 2022-12-07-file-descriptor %})

<br/>
<br/>
## References
- [https://en.wikipedia.org/wiki/Network_socket](https://en.wikipedia.org/wiki/Network_socket)
- [https://en.wikipedia.org/wiki/Internet_protocol_suite](https://en.wikipedia.org/wiki/Internet_protocol_suite)
- [https://en.wikipedia.org/wiki/Transport_layer](https://en.wikipedia.org/wiki/Transport_layer)
- [https://en.wikipedia.org/wiki/File_descriptor](https://en.wikipedia.org/wiki/File_descriptor)
- [https://en.wikipedia.org/wiki/Port_(computer_networking)](https://en.wikipedia.org/wiki/Port_(computer_networking))