---
title     : Study GFS
date      : 2015-09-25
---

We have also introduced an atomic append operation so that multiple clients can append concurrently to a file without extra synchronization between them.

We support the usual operations to create, delete, open, close, read, and write files.
Moreover, GFS has snapshot and record append operations.

Clients do cache metadata， do not cache data.

GFS achieves this by
  (a) applying mutations to a chunk in the same order on all its replicas
  (b) using chunk version numbers to detect any replica that has become stale because it has missed mutations while its chunkserver was down

The master grants a chunk lease to one of the repli- cas, which we call the primary. The primary picks a serial order for all mutations to the chunk. All replicas follow this order when applying mutations. 
