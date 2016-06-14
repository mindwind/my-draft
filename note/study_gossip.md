---
title     : Study Gossip
date      : 2016-06-02
---


## [1]
The key requirement is that the aggregate must be computable by fixed-size pairwise information exchanges; these typically terminate after a number of rounds of information exchange logarithmic in the system size, by which time an all-to-all information flow pattern will have been established.

Typically gossip protocols are those that specifically run in a regular, periodic, relatively lazy, symmetric and decentralized manner;


## [2]
Nodes are classified as being __infective__, __susceptible__ and __removed__.
__infective__:   will try to spread some information by periodically selecting a random peer from the network.
__susceptible__: it doesn’t know about said information, then it will become infected, and thus will also start to try to spread this particular information to other nodes.
__removed__:     one that knows about the new piece of information that circulating around, but it’s not spreading it.


## [3]
In general, it takes O(logN) rounds to reach all nodes, where N is the number of nodes. A round completes when every peer has initiated a gossip
exactly once.


## [4]
Cycles   = log(N) + ln(N) + O(1)
Messages = O(NlogN)    the number of overall messages sent.


## [5]
__Susceptible__ if p has not yet received an update
__Infective__   if p holds an update it is willing to share
__Removed__     if p has the update but is no longer willing to share it


## References
[1]. Wikipedia. [Gossip protocol](https://en.wikipedia.org/wiki/Gossip_protocol). 2016.03.29
[2]. ALVARO VIDELA. [GOSSIP PROTOCOLS, WHERE TO START](http://videlalvaro.github.io/2015/12/gossip-protocols.html). 2015.12.02
[3]. Anne-Marie et al. [Gossiping in Distributed Systems](http://www.distributed-systems.net/papers/2007.osr.pdf). 2007
[4]. Márk Jelasity. [Gossip Protocols ](http://www.inf.u-szeged.hu/~jelasity/ddm/gossip.pdf)
[5]. Alberto Montresor. [Gossip protocols for large-scale distributed systems](http://sbrc2010.inf.ufrgs.br/resources/presentations/tutorial/tutorial-montresor.pdf). 2010
