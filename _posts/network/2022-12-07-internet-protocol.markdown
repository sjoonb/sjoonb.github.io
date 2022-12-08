---
layout: post
title:  "Internet Protocol"
categories: network
date:  2022-12-07 15:12:25 +0900
---




The **Internet Protocol (IP)** is the network layer communications protocol in the Internet protocol suite for relaying datagrams across network boundaries. Its routing function enables internetworking, and essentially establishes the Internet.

IP has the task of delivering packets from the source host to the destination host solely based on the IP addresses in the packet headers. For this purpose, IP defines packet structures that encapsulate the data to be delivered. It also defines addressing methods that are used to label the datagram with source and destination information.

The first major version of IP, Internet Protocol Version 4 (**IPv4**), is the dominant protocol of the Internet. Its successor is Internet Protocol Version 6 (**IPv6**), which has been in increasing deployment on the public Internet since c. 2006.

IP addresses are written and displayed in human-readable notations, such as 192.0.2.1 in **IPv4**, and 2001:db8:0:1234:0:567:8:1 in **IPv6**


<br/>

- [Function](#function)
- [subnetworks](#subnetworks)


<br/>
## Function

The Internet Protocol is responsible for **addressing host interfaces**, **encapsulating data into datagrams** (including fragmentation and reassembly) and **routing datagrams from a source host interface to a destination host** interface across one or more IP networks. For these purposes, the Internet Protocol defines the format of packets and provides an addressing system.

Each datagram has two components: a **header** and a **payload**. The IP header includes source IP address, destination IP address, and other metadata needed to route and deliver the datagram. The payload is the data that is transported. This method of nesting the data payload in a packet with a header is called **encapsulation**.

IP addressing entails the assignment of IP addresses and associated parameters to host interfaces. The address space is divided into [subnetworks](#subnetworks), involving the designation of network prefixes. IP routing is performed by all hosts, as well as `routers`, whose main function is to transport packets across network boundaries. Routers communicate with one another via specially designed **routing protocols**, either interior gateway protocols or exterior gateway protocols, as needed for the topology of the network.



<br/>
## subnetworks

<br/>
![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/14/Subnetting_Concept-en.svg/600px-Subnetting_Concept-en.svg.png)

*Creating a subnet by dividing the host identifier*

<br/>
A **subnetwork** or **subnet** is a logical subdivision of an IP network. The practice of dividing a network into two or more networks is called **subnetting**.

For **IPv4**, a network may also be characterized by its **subnet mask** or **netmask**, which is the `bitmask` that, when applied by a `bitwise AND` operation to any IP address in the network, yields the routing prefix. Subnet masks are also expressed in `dot-decimal notation` like an IP address. For example, the prefix 198.51.100.0/24 would have the subnet mask 255.255.255.0.

The **benefits of subnetting** an existing network vary with each deployment scenario. In the address allocation architecture of the Internet using CIDR and in large organizations, it is necessary to allocate address space efficiently. Subnetting may also enhance routing efficiency, or have advantages in network management when subnetworks are administratively controlled by different entities in a larger organization. Subnets may be arranged logically in a hierarchical architecture, partitioning an organization's network address space into a tree-like routing structure, or other structures such as meshes.

<br/>
<br/>
References

- [https://en.wikipedia.org/wiki/Internet_Protocol](https://en.wikipedia.org/wiki/Internet_Protocol)
- [https://en.wikipedia.org/wiki/Subnetwork](https://en.wikipedia.org/wiki/Subnetwork)
- [https://en.wikipedia.org/wiki/Port_(computer_networking)](https://en.wikipedia.org/wiki/Port_(computer_networking))