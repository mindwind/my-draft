---
title     : 《大规模分布式存储系统》 读书笔记
date      : 2015-08-07
---

## 1. 概述


## 2. 单机存储引擎
### 脉络
  - 哈希存储引擎  Bitcask
  - B树存储引擎   MySQL InnoDB
  - LSM（Log Structured Merge Tree）树存储引擎  Google Bigtable、Google LevelDB、Cassandra

### 批注
LSM树的优势在于有效地规避了磁盘随机写入问题，但读取时可能需要访问较多的磁盘文件。

1977年，以色列人Jacob Ziv和Abraham Lempel发表论文《顺序数据压缩的一个通用算法》，从此，
LZ系列压缩算法几乎垄断了通用无损压缩领域，常用的Gzip算法中使用的LZ77，GIF图片格式中使用的LZW，
以及LZO等压缩算法都属于这个系列。


## 3. 分布式系统
### 脉络
  - 分布（数据分布均匀，负载均衡）
  - 可靠（副本、复制，一致性）
  - 性能（吞吐和延时估算）
  - 容错（故障类型、检测和恢复）
  - 扩展（总控模型、P2P）
