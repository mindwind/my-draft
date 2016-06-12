---
title     : Study Gossip
date      : 2016-06-02
---


The key requirement is that the aggregate must be computable by fixed-size pairwise information exchanges; these typically terminate after a number of rounds of information exchange logarithmic in the system size, by which time an all-to-all information flow pattern will have been established.[1］

Typically gossip protocols are those that specifically run in a regular, periodic, relatively lazy, symmetric and decentralized manner; [1]

In general, it takes O(logN) rounds to reach all nodes, where N is the number of nodes. A round completes when every peer has initiated a gossip
exactly once. [3]


## References
[1]. Wikipedia. [Gossip protocol](https://en.wikipedia.org/wiki/Gossip_protocol). 2016.03.29
[2]. ALVARO VIDELA. [GOSSIP PROTOCOLS, WHERE TO START](http://videlalvaro.github.io/2015/12/gossip-protocols.html). 2015.12.02
[3]. Anne-Marie et al. [Gossiping in Distributed Systems](http://www.distributed-systems.net/papers/2007.osr.pdf).  2007
