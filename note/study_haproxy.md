---
title     : Study HAProxy
date      : 2016-02-17
---


## Architecture
HAProxy is a single-threaded, event-driven, non-blocking daemon. This means is
uses event multiplexing to schedule all of its activities instead of relying on
the system to schedule between multiple activities.

HAProxy is designed to isolate itself into a chroot jail during startup, where
it cannot perform any file-system access at all. The immediate effect is that
a running process will not be able to reload a configuration file to apply
changes, instead a new process will be started using the updated configuration
file.

HAProxy is a TCP proxy, not a router. It deals with established connections that
have been validated by the kernel, and not with packets of any form nor with
sockets in other states

HAProxy doesn't write log files, but it relies on the standard syslog protocol
to send logs to a remote server.

## Stop & Restart & reload
HAProxy supports a graceful and a hard stop. The hard stop is simple, when the
SIGTERM signal is sent to the haproxy process, it immediately quits and all
established connections are closed.The graceful stop is triggered when the
SIGUSR1 signal is sent to the haproxy process. It consists in only unbinding
from listening ports, but continue to process existing connections until they
close. Once the last connection is closed, the process leaves.

HAProxy tries to bind to all listening ports.If a socket binding fails because a port is already in use, then
the process will first send a SIGTTOU signal.This is what is called the "pause" signal. It instructs
all existing haproxy processes to temporarily stop listening to their ports so
that the new process can try to bind again. During this time, the old process
continues to process existing connections. If the binding still fails then the new process sends a
SIGTTIN signal to the old processes to instruct them to resume operations just
as if nothing happened. The old processes will then restart listening to the
ports and continue to accept connections.

It is important to note that during this timeframe, there are two small windows
of a few milliseconds each where it is possible that a few connection failures
will be noticed during high loads.

HAProxy works around this on systems that support the SO_REUSEPORT socket options, as it allows the new process to bind without first asking the old one to unbind. Most BSD systems have been supporting this almost forever. Linux has been supporting this in version 2.0 and dropped it around 2.2, but some patches were floating around by then. It was reintroduced in kernel 3.9.


## epoll & kqueue
For Linux systems base on kernels 2.6 and above, the epoll() system call will
be used. It's a much more scalable mechanism relying on callbacks in the kernel
that guarantee a constant wake up time regardless of the number of registered
monitored file descriptors.

For BSD systems which support it, kqueue() is available as an alternative. It
is much faster than poll() and even slightly faster than epoll() thanks to its
batched handling of changes. At least FreeBSD and OpenBSD support it.


## Memory Management
HAProxy uses a simple and fast pool-based memory management. Since it relies on
a small number of different object types, it's much more efficient to pick new
objects from a pool which already contains objects of the appropriate size than
to call malloc() for each different size. The pools are organized as a stack or
LIFO, so that newly allocated objects are taken from recently released objects
still hot in the CPU caches. Pools of similar sizes are merged together, in
order to limit memory fragmentation.


## CPU
But with heavily network-bound workloads
it is the opposite as the haproxy process will have to fight against its kernel
counterpart. Pinning haproxy to one CPU core and the interrupts to another one,
all sharing the same L3 cache tends to sensibly increase network performance
because in practice the amount of work for haproxy and the network stack are
quite close, so they can almost fill an entire CPU each.

For CPU-bound workloads consisting in a lot of SSL traffic or a lot of
compression, it may be worth using multiple processes dedicated to certain
tasks


## logging
For logging, HAProxy always relies on a syslog server since it does not perform
any file-system access. The standard way of using it is to send logs over UDP
to the log server (by default on port 514).


## issue
the TCP congestion window may be limited and not allow these data to leave, waiting for
an ACK to open the window. If the traffic is idle and the data take 40 ms or
200 ms to leave, it's a different issue (which is not an issue), it's the fact
that the Nagle algorithm prevents empty packets from leaving immediately, in
hope that they will be merged with subsequent data.

HAProxy automatically disables Nagle in pure TCP mode and in tunnels. However it definitely remains
enabled when forwarding an HTTP body.Some HTTP non-compliant
applications may be sensitive to the latency when delivering incomplete HTTP
response messages. In this case you will have to enable "option http-no-delay"
to disable Nagle in order to work around their design, keeping in mind that any
other proxy in the chain may similarly be impacted.


## load balancing
L4
Acts at the packet level and processes packets more or less individually.

L7
It requires that the input streams is reassembled and processed as a whole.
The contents may be modified, and the output stream is segmented into new packets.
This implies that there are two distinct connections on each side.


## Features
Provide the server with a clean connection to protect them against any client-side defect or attack;
Optimize TCP stacks (eg: SACK), congestion control, and reduce RTT impacts;


## Why
SSL LB
a single software-based load balancer will not be faster to process SSL than an eight-servers farm. Because of this architectural error, the load balancer will saturate before the application servers, and the only remedy will be to put another level of load balancers in front of it, and adding more load balancers to handle the SSL load. Obviously, this is wrong.The most scalable solution when applications require SSL is to dedicate a farm of reverse-proxies only for this matter.



## 参考
[1] HAProxy Documentation. [HAProxy Management Guide](http://www.haproxy.org/download/1.6/doc/management.txt)
[2] HAProxy Documentation. [HAProxy Starter Guide](http://cbonte.github.io/haproxy-dconv/intro-1.6.html)
[3] Willy Tarreau. [Making applications scalable with Load Balancing](http://1wt.eu/articles/2006_lb/index.html)
