# 分布式系统学习

## 1. 理论部分
### 数据结构

~~B-Tree~~

~~Log Merge Tree~~

### 算法和协议
Byzantine General

~~paxos~~

~~raft~~

~~MapReduce~~

MapReduce: Simplified Data Processing on Large Clusters

https://www12.informatik.uni-erlangen.de/edu/map/ss10/talks/MapReduce.pdf

MapReduce: A major step backwards

https://homes.cs.washington.edu/~billhowe/mapreduce_a_major_step_backwards.html

~~CAP-BASE-ACID~~

~~2PC & 3PC~~

~~gossip~~

### 状态和时序
~~Time Clocks and the Ordering of Events in a Distributed System~~

~~Virtual Time and Global States of Distributed System~~

~~Distributed Snapshots: Determining Global States of a Distributed System~~


## 2. 分布式基础设施
### 消息队列
~~RabbitMQ~~

### 分布式锁服务、协调
~~Chubby~~

~~Zookeeper~~


## 3. 分布式键值系统
### memcached

### redis

### Amazon Dynamo

Dynamo: Amazon’s Highly Available Key-value Store
http://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf
### Taobao Tair

## 4. 分布式文件系统

### GFS
The Google File System
http://www.eecg.toronto.edu/~ashvin/courses/ece1746/2003/reading/ghemawat-sosp03.pdf
### Taobao TFS
### Facebook Haystack

### ~~HDFS~~ almost finish

### Ceph

https://www.ssrc.ucsc.edu/Papers/weil-osdi06.pdf

https://www.ibm.com/developerworks/cn/linux/l-ceph/index.html

## 5. 分布式表格系统

### Bigtable
Bigtable: A Distributed Storage System for Structured Data
http://lintool.github.io/UMD-courses/bigdata-2015-Spring/content/ChangFay_etal_OSDI2006.pdf
### ~~Megastore~~

### ~~Azure Storage~~


## 6. 分布式数据库
### MySQL Sharding
### OceanBase
### ~~Spanner~~
Spanner: Google’s Globally-Distributed Database
https://www.usenix.org/conference/osdi12/technical-sessions/presentation/corbett
https://www.usenix.org/system/files/conference/osdi12/osdi12-final-16.pdf
### ~~Azure SQL server~~



----------

## 参考

### 其他学习资料
awesome-distributed-systems

https://github.com/zhenlohuang/awesome-distributed-systems

分布式系统(Distributed System)资料
https://github.com/ty4z2008/Qix/blob/master/ds.md

### 课程
CMU分布式系统入门课 15-440/640, Spring 2014: Distributed Systems
http://www.cs.cmu.edu/~dga/15-440/S14/

15-712 Advanced and Distributed Operating Systems, Spring 2012
http://www.cs.cmu.edu/afs/cs.cmu.edu/academic/class/15712-s12/www/

MIT 15-640/440 Lecture Resources
https://www.andrew.cmu.edu/course/15-440-s13/index/lecture_index.html

## papers
[1] Paxos Made Simple
https://www.microsoft.com/en-us/research/publication/paxos-made-simple/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Flamport%2Fpubs%2Fpaxos-simple.pdf
http://zoo.cs.yale.edu/classes/cs426/2012/bib/lamport01paxos.pdf

[2] Multi-Paxos和Raft的资料：Raft user study
https://ramcloud.stanford.edu/~ongaro/userstudy/

[3] Distributed systemsfor fun and profit
http://book.mixu.net/distsys/

[4] Distributed systems theory for the distributed systems engineer
http://the-paper-trail.org/blog/distributed-systems-theory-for-the-distributed-systems-engineer/

[5] Introduction to HBase Schema Design
http://lintool.github.io/UMD-courses/bigdata-2015-Spring/content/Khurana_etal_2012.pdf

[6] Consistency Tradeoffs in Modern Distributed Database System Design
http://lintool.github.io/UMD-courses/bigdata-2015-Spring/content/Abadi_2012.pdf

[7] F1: A Distributed SQL Database That Scales
http://www.vldb.org/pvldb/vol6/p1068-shute.pdf

[8] Tachyon: Reliable, Memory Speed Storage for Cluster Computing
https://www2.eecs.berkeley.edu/Pubs/TechRpts/2014/EECS-2014-135.pdf

[9] RAMCloud: A Low-Latency Datacenter Storage System
http://www.hpcadvisorycouncil.com/events/2013/Stanford-Workshop/pdf/Presentations/Day%201/10_Stanford_RAMcloud.pdf

[10] Cassandra - A Decentralized Structured Storage System
http://www.ijetjournal.org/Special-Issues/ICETAC2K17-2/ICETAC2K17-P122.pdf

[11] MapReduce and Parallel DBMSs: Friends or Foes?
http://lintool.github.io/UMD-courses/bigdata-2015-Spring/content/Stonebraker_etal_CACM2010.pdf

[12] A comparison of approaches to large scale data analysis
http://www.cs.cmu.edu/~pavlo/courses/fall2013/static/slides/mapreduce.pdf

[13] Sinfonia: a new paradigm for
building scalable distributed systems
http://www.sosp2007.org/papers/sosp064-aguilera.pdf

[14] How does a relational database work - Coding Geek
http://coding-geek.com/how-databases-work/

[15] 分式系统工程实践
https://wenku.baidu.com/view/895a2a3467ec102de2bd8902?pcf=2#page/1/1375282274254

[16] 用大白话聊聊分布式系统
https://waylau.com/talk-about-distributed-system/

[17]  《这就是搜索引擎--核心技术详解》
