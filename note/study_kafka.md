---
title     : Study Kafka
date      : 2015-10-23
---

 For each topic, the Kafka cluster maintains a partitioned log.

 Each partition has one server which acts as the "leader" and zero or more servers which act as "followers".

 The messages in the partitions are each assigned a sequential id number called the offset that uniquely identifies each message within the partition.

 Each server acts as a leader for some of its partitions and a follower for others so load is well balanced within the cluster.

 The producer is responsible for choosing which message to assign to which partition within the topic.
 Kafka only provides a total order over messages within a partition, not between different partitions in a topic.

 Efficient compression requires compressing multiple messages together rather than compressing each message individually.


## References
  1. [Kafka Documentation](http://kafka.apache.org/documentation.html)
