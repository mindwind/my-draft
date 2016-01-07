---
title     : Study MongoDB
date      : 2015-12-30
---


[1] MongoDB Doc. [MongoDB Manual](https://docs.mongodb.org/manual/)
[2] MongoDB White Paper. [MongoDB Architecture Guide](http://s3.amazonaws.com/info-mongodb-com/MongoDB_Architecture_Guide.pdf)

## Key Features
High Performance
 - Support for embedded data models reduces I/O activity on database system.
 - Indexes support faster queries and can include keys from embedded documents and arrays.

High Availability
To provide high availability, MongoDB’s replication facility, called replica sets, provide:

  - automatic failover.
  - data redundancy.

Automatic Scaling
  - Automatic sharding distributes data across a cluster of machines.
  - Replica sets can provide eventually-consistent reads for low-latency high throughput deployments.


## FAQ
Does MongoDB support transactions?
MongoDB does not support multi-document transactions. However, MongoDB does provide atomic operations on a single document.


## Data model
In MongoDB, write operations are atomic at the document level 如何实现的？

Power of 2 Sized Allocations
No Padding Allocation Strategy


## Architecture Guide
Each query can specify the appropriate write concern, ranging from unacknowledged to acknowledgement that writes have been committed to all replicas.


## Storage Engine
  - WiredTiger uses document-level concurrency control for write operations. As a result, multiple clients can modify different documents of a collection at the same time.
    compression algorithms: Snappy, zlib,
  - MMAPv1 is MongoDB’s original storage engine based on memory mapped files. It excels at workloads with high volume inserts, reads, and in-place updates.
  - In-Memory beta

## sharding
MongoDB distributes data, or shards, at the collection level.
A shard key is either an indexed field or an indexed compound field that exists in every document in the collection. MongoDB divides the shard key values into chunks and distributes the chunks evenly across the shards.

Primary Shard
Every database has a “primary” [1] shard that holds all the un-sharded collections in that database.

Shard keys are immutable and cannot be changed after insertion.

MongoDB briefly pauses all application writes to the source shard before updating the config servers with the new location for the chunk, and resumes the application writes after the update.


[3] 陈皓. [千万别用MongoDB？真的吗？](http://coolshell.cn/articles/5826.html). 2011.11


[4] David Mytton. [Does everyone hate MongoDB?](https://blog.serverdensity.com/does-everyone-hate-mongodb/). 2012.09
With any product, if you decide to deploy it to production you need to be sure you fully understand its architecture and scaling profile.


[5] David Mytton. [MongoDB Benchmarks](https://blog.serverdensity.com/mongodb-benchmarks/). 2012.08
Putting your journal on an SSD and then using the j=1 flag is a good optimisation.
What this experiment shows is the differences between the write concern options so you can make the right tradeoff between durability and performance.

[6] David Mytton. [MongoDB schema design pitfalls](https://blog.serverdensity.com/mongodb-schema-design-pitfalls/). 2013.02
Remember, “schemaless” doesn’t mean you don’t need to design your schema.
so just like any database, to improve performance and make things scale, you still have to think about schema design.
People misinterpret @mongodb scalability. It’s not easy per se, it’s just easier. Still requires thought, understanding and testing
