---
title: "Databases for Big Data"
date: 2020-12-01T18:22:00+08:00
image: 'p4.png'
---

# Databases for Big Data

Nosql databases are very popular in industry nowadays, including Redis and HBase. Redis is one example of so-called No-sql, which means database that is not relational, and it stores the data in Key-Value format. HBase is a distributed scalable database, which is a part of Hadoop ecology.
A brief introduction about what are these and how to use these tools to cope with the challenge brought by the big data era will be given here.




## Redis Overview

Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes with radius queries and streams. Redis has built-in replication, Lua scripting, LRU eviction, transactions and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster. Redis also supports various atomic operations on these types, like appending to a string; incrementing the value in a hash; pushing an element to a list; computing set intersection, union and difference; or getting the member with highest ranking in a sorted set.

Redis popularized the idea of a system that can be considered at the same time a store and a cache, using a design where data is always modified and read from the main computer memory, but also stored on disk in a format that is unsuitable for random access of data, but only to reconstruct the data back in memory once the system restarts. At the same time, Redis provides a data model that is very unusual compared to a relational database management system (RDBMS). User commands do not describe a query to be executed by the database engine but rather specific operations that are performed on given abstract data types. Hence, data must be stored in a way which is suitable later for fast retrieval, without help from the database system in form of secondary indexes, aggregations or other common features of traditional RDBMS.

In order to achieve its outstanding performance, Redis works with an in-memory dataset. Depending on your use case, you can persist it either by dumping the dataset to disk every once in a while, or by appending each command to a log. Persistence can be optionally disabled, if you just need a feature-rich, networked, in-memory cache. 

Redis also supports trivial-to-setup master-slave asynchronous replication, with very fast non-blocking first synchronization, auto-reconnection with partial resynchronization on net split. Redis also supports other features include:

- Transactions
- Pub/Sub
- Lua scripting
- Keys with a limited time-to-live
- LRU eviction of keys
- Automatic failover

However, there is still some limitation regrading to Redis. For example, since Redis is an in-memory store with some persistency capabilities, all the dataset should fit in memory of the server; therefore, a single instance is limited by the maximum memory of your server. Due to its high-speed data io efficiency, Redis is still a good solution for caching, and it's possible to store a fragmentation of data for frequent use and access on Redis. But Redis is not suitable for storing the whole data, because a single Redis instance is not a distributed system but a remote centralized store. To solve this, people can use Redis to build a distributed storage system, and run it on a cluster.



## Apache HBase Overview

Apache HBase is the Hadoop database, a distributed, scalable, big data store. Apache HBase is used when people need random, realtime read/write access to your Big Data. This goal of Apache HBase project is the hosting of very large tables -- billions of rows X millions of columns -- atop clusters of commodity hardware. It is an open-source, distributed, versioned, non-relational database modeled after Google's Bigtable: A Distributed Storage System for Structured Data by Chang et al. Just as Bigtable leverages the distributed data storage provided by the Google File System, Apache HBase provides Bigtable-like capabilities on top of Hadoop and HDFS.

HBase is an open-source non-relational distributed database modeled after Google's Bigtable and written in Java. It is developed as part of Apache Software Foundation's Apache Hadoop project and runs on top of HDFS (Hadoop Distributed File System), providing Bigtable-like capabilities for Hadoop. That is, it provides a fault-tolerant way of storing large quantities of sparse data (small amounts of information caught within a large collection of empty or unimportant data, such as finding the 50 largest items in a group of 2 billion records, or finding the non-zero items representing less than 0.1% of a huge collection).

HBase features compression, in-memory operation, and Bloom filters on a per-column basis as outlined in the original Bigtable paper. Tables in HBase can serve as the input and output for MapReduce jobs run in Hadoop, and may be accessed through the Java API but also through REST, Avro or Thrift gateway APIs. HBase is a wide-column store and has been widely adopted because of its lineage with Hadoop and HDFS. HBase runs on top of HDFS and is well-suited for faster read and write operations on large datasets with high throughput and low input/output latency.

HBase is not a direct replacement for a classic SQL database, however Apache Phoenix project provides a SQL layer for HBase as well as JDBC driver that can be integrated with various analytics and business intelligence applications. The Apache Trafodion project provides a SQL query engine with ODBC and JDBC drivers and distributed ACID transaction protection across multiple statements, tables and rows that use HBase as a storage engine.

