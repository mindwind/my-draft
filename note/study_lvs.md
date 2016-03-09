---
title     : Study LVS
date      : 2016-03-09
---


## Load balancing
In computing, load balancing is a technique used to spread work load among many processes, computers, networks, disks or other resources, so that no single resource is overloaded.

IP load balancing techniques
In the VS/TUN and VS/DR clusters, the Virtual IP (VIP) addresses are shared by both the load balancer and real servers, because they all configure the VIP address on one of their interfaces.
In the VS/TUN and VS/DR cluster, we must guarantee that only the load balancer answers arp request for the VIP to accept incoming packets for virtual service, and the real servers(in the same network of load balancer) don't answer arp request for the VIP but can process packets destined for the VIP locally.


### NAT
Network Address Translation is a feature by which IP addresses are mapped from one group to another. When the address mapping is N-to-N, it is called static network address translation; when the mapping is M-to-N (M>N), it is called dynamic network address translation.

how
The load balancer examines the packet's destination address and port number. If they are matched for a virtual server service according to the virtual server rule table, a real server is chosen from the cluster by a scheduling algorithm, and the connection is added into the hash table which record the _established connection_. Then, the destination address and the port of the packet are _rewritten_ to those of the chosen server, and the packet is forwarded to the server.When the incoming packet belongs to this connection and the chosen server can be found in the hash table, the packet will be rewritten and forwarded to the chosen server.

advantage
real servers can run any operating system that supports TCP/IP protocol, real servers can use private Internet addresses.

disadvantage
the scalability of the virtual server via NAT is limited, The load balancer may be a bottleneck of the whole system when the number of server nodes (general PC servers) increase to around 20 or more.


### IP Tunneling
IP tunneling (IP encapsulation) is a technique to encapsulate IP datagram within IP datagrams, which allows datagrams destined for one IP address to be wrapped and redirected to another IP address.

how
The load balancer examines the packet's destination address and port. If they are matched for the virtual service, a real server is chosen from the cluster according to a connection scheduling algorithm, and the connection is added into the hash table which records connections. Then, the load balancer encapsulates the packet within an IP datagram and forwards it to the chosen server.
the <Virtual IP Address> must be configured on non-arp devices or any alias of non-arp devices, or the system can be configured to redirect packets for <Virtual IP Address> to a local socket

advantage
the load balancer just schedules requests to the different real servers, and the real servers return replies directly to the users. So, the load balancer can handle huge amount of requests, it may schedule over 100 real servers.

disadvantage
all servers must have "IP Tunneling"(IP Encapsulation) protocol enabled.


### Direct Routing
The virtual IP address is shared by real servers and the load balancer.

how
The load balancer simply changes the MAC address of the data frame to that of the chosen server and restransmits it on the LAN. This is the reason that the load balancer and each server must be directly connected to one another by a single uninterrupted segment of a LAN.

advantage
highest performance.

disadvantage
Compared to the virtual server via IP tunneling approach, this approach doesn't have tunneling overhead(In fact, this overhead is minimal in most situations), but requires that one of the load balancer's interfaces and the real servers' interfaces must be in the same physical segment


## 参考
[1] LVS wiki. [Load balancing](http://kb.linuxvirtualserver.org/wiki/Load_balancing)
[2] HAProxy Documentation. [HAProxy Starter Guide](http://cbonte.github.io/haproxy-dconv/intro-1.6.html)
[3] Willy Tarreau. [Making applications scalable with Load Balancing](http://1wt.eu/articles/2006_lb/index.html)
