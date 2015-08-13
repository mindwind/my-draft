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

DataNodes
  - manage storage, a file is split into one or more blocks and these blocks are stored in a set of DataNodes
  - all blocks in a file except the last block are the same size.
  - responsible for serving read and write requests from the file system’s clients
  - perform block creation, deletion, and replication upon instruction from the NameNode.


## Data Replication
For the common case, when the replication factor is three, HDFS’s placement policy is to put one replica on one node in the local rack, another on a different node in the local rack, and the last on a different node in a different rack.

HDFS tries to satisfy a read request from a replica that is closest to the reader.

On startup, the NameNode enters a special state called Safemode.
Replication of data blocks does not occur when the NameNode is in the Safemode state.
