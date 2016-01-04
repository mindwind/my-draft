---
title     : Study MongoDB
date      : 2015-12-30
---


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


## Architecture Guide
Each query can specify the appropriate write concern, ranging from unacknowledged to acknowledgement that writes have been committed to all replicas.


## Storage Engine
  - WiredTiger uses document-level concurrency control for write operations. As a result, multiple clients can modify different documents of a collection at the same time.
    compression algorithms: Snappy, zlib,
  - MMAPv1 is MongoDB’s original storage engine based on memory mapped files. It excels at workloads with high volume inserts, reads, and in-place updates.
  - In-Memory beta


## 参考
[1] MongoDB White Paper. [MongoDB Architecture Guide](http://s3.amazonaws.com/info-mongodb-com/MongoDB_Architecture_Guide.pdf)
