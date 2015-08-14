---
title     : Study HDFS
date      : 2015-08-13
---


## Assumptions and Goals
Hardware failure is the normal rather than the exception. Therefore, detection of faults and quick, automatic recovery from them is a core architectural goal of HDFS.

A typical file in HDFS is gigabytes to terabytes in size.
It should support tens of millions of files in a single instance.

HDFS applications need a write-once-read-many access model for files.
A file once created, written, and closed need not be changed.


## NameNode and DataNodes
NameNode
  - HDFS cluster consists of a single NameNode
  - manages the file system namespace and regulates access to files by clients
  - executes file system namespace operations like opening, closing, and renaming files and directories.
  - the arbitrator and repository for all HDFS metadata
  - The number of copies of a file is called the replication factor, this information is stored by the NameNode.

优化并发下写事务
The NameNode is a multithreaded system and processes requests simultaneously from multiple clients. Saving a transaction to disk becomes a bottleneck since all other threads need to wait until the synchronous flush-and-sync procedure initiated by one of them is complete. In order to optimize this process, the NameNode batches multiple transactions. When one of the NameNode's threads initiates a flush-and-sync operation, all the transactions batched at that time are committed together. Remaining threads only need to check that their transactions have been saved and do not need to initiate a flush-and-sync operation.

DataNodes
  - manage storage, a file is split into one or more blocks and these blocks are stored in a set of DataNodes
  - all blocks in a file except the last block are the same size.
  - responsible for serving read and write requests from the file system’s clients
  - perform block creation, deletion, and replication upon instruction from the NameNode.

block 实现方式
Each block replica on a DataNode is represented by two files in the local native filesystem. The first file contains the data itself and the second file records the block's metadata including checksums for the data and the generation stamp.

namespace ID：全局标记集群，同一 cluster 共享一个；一个新初始化的 DataNode 加入集群时没有 namespace ID，和 NameNode 握手结束后分配给它
storage ID：DataNode 的内部唯一标记，也是在和 NameNode 首次握手结束后分配，之后不再改变

DataNode 的默认 heartbeat 间隔是 3 秒；为什么这么短？
The NameNode does not directly send requests to DataNodes. It uses replies to heartbeats to send instructions to the DataNodes.
The instructions include commands to replicate blocks to other nodes, remove local block replicas, re-register and send an immediate block report, and shut down the node.


## Data Replication
For the common case, when the replication factor is three, HDFS’s placement policy is to put one replica on one node in the local rack, another on a different node in the local rack, and the last on a different node in a different rack.

HDFS tries to satisfy a read request from a replica that is closest to the reader.

On startup, the NameNode enters a special state called Safemode.
Replication of data blocks does not occur when the NameNode is in the Safemode state.

对热点文件可以提供更多副本以增强容错性和增加读取带宽
For critical files or files which are accessed very often, having a higher replication factor improves tolerance against faults and increases read bandwidth.


## The Persistence of File System Metadata
The NameNode uses a transaction log called the EditLog to persistently record every change that occurs to file system metadata.The entire file system namespace, including the mapping of blocks to files and file system properties, is stored in a file called the FsImage.

When the NameNode starts up, it reads the FsImage and EditLog from disk, applies all the transactions from the EditLog to the in-memory representation of the FsImage, and flushes out this new version into a new FsImage on disk. It can then truncate the old EditLog because its transactions have been applied to the persistent FsImage. This process is called a checkpoint.

The DataNode stores HDFS data in files in its local file system. It stores each block of HDFS data in a separate file in its local file system. The DataNode does not create all files in the same directory. Instead, it uses a heuristic to determine the optimal number of files per directory and creates subdirectories appropriately.


## Robustness
The NameNode marks DataNodes without recent Heartbeats as dead and does not forward any new IO requests to them.
DataNode death may cause the replication factor of some blocks to fall below their specified value.
Re-replication may arise due to many reasons: a DataNode may become unavailable, a replica may become corrupted, a hard disk on a DataNode may fail, or the replication factor of a file may be increased.

The HDFS client software implements checksum checking on the contents of HDFS files. When a client creates an HDFS file, it computes a checksum of each block of the file and stores these checksums in a separate hidden file in the same HDFS namespace.


## Data Organization
Data blocks: A typical block size used by HDFS is 64 MB.
HDFS client caches the file data into a temporary local file. Application writes are transparently redirected to this temporary local file. When the local file accumulates data worth over one HDFS block size, the client contacts the NameNode. The NameNode inserts the file name into the file system hierarchy and allocates a data block for it.

When a file is closed, the remaining un-flushed data in the temporary local file is transferred to the DataNode.
When a file is closed, the remaining un-flushed data in the temporary local file is transferred to the DataNode. The client then tells the NameNode that the file is closed. At this point, the NameNode commits the file creation operation into a persistent store. If the NameNode dies before the file is closed, the file is lost.

Replication Pipelining


## Space Reclamation
File Deletes
HDFS first renames it to a file in the /trash directory. A file remains in /trash for a configurable amount of time. After the expiry of its life in /trash, the NameNode deletes the file from the HDFS namespace.

Decrease Replication Factor
When the replication factor of a file is reduced,  The next Heartbeat transfers this information to the DataNode.


## References
  1. [HDFS Architecture](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html)
