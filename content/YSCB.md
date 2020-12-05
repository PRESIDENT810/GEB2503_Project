---
title: "YSCB: Yahoo Cloud Serving Benchmark"
date: 2020-12-01T20:57:16+08:00
draft: true
image: 'p6.png'
---

## YSBC Overview

The Yahoo! Cloud Serving Benchmark (YCSB) is an open-source specification and program suite for evaluating retrieval and maintenance capabilities of computer programs. It is often used to compare relative performance of NoSQL database management systems.

The original benchmark was developed by workers in the research division of Yahoo! who released it in 2010 with the stated goal of "facilitating performance comparisons of the new generation of cloud data serving systems", particularly for transaction-processing workloads which differed from ones measured by benchmarks designed for more traditional database management systems.

The goal of the YCSB project is to develop a framework and common set of workloads for evaluating the performance of different “key-value” and “cloud” serving stores. The project comprises two things:

- The YCSB Client, an extensible workload generator
- The Core workloads, a set of workload scenarios to be executed by the generator

Although the core workloads provide a well rounded picture of a system’s performance, the Client is extensible so that you can define new and different workloads to examine system aspects, or application scenarios, not adequately covered by the core workload. Similarly, the Client is extensible to support benchmarking different databases. Although we include sample code for benchmarking HBase, Cassandra, Infinispan and MongoDB, it is straightforward to write a new interface layer to benchmark your favorite database.
A common use of the tool is to benchmark multiple systems and compare them. For example, you can install multiple systems on the same hardware configuration, and run the same workloads against each system. Then you can plot the performance of each system (for example, as latency versus throughput curves) to see when one system does better than another.



### Workloads

YCSB includes a set of core workloads that define a basic benchmark for cloud systems. Of course, you can define your own workloads, as described in Implementing New Workloads. However, the core workloads are a useful first step, and obtaining these benchmark numbers for a variety of different systems would allow you to understand the performance tradeoffs of different systems.  

The core workloads consist of six different workloads:

- **Workload A: Update heavy workload**

This workload has a mix of 50/50 reads and writes. An application example is a session store recording recent actions.

- **Workload B: Read mostly workload**

This workload has a 95/5 reads/write mix. Application example: photo tagging; add a tag is an update, but most operations are to read tags.

- **Workload C: Read only**

This workload is 100% read. Application example: user profile cache, where profiles are constructed elsewhere (e.g., Hadoop).

- **Workload D: Read latest workload**

In this workload, new records are inserted, and the most recently inserted records are the most popular. Application example: user status updates; people want to read the latest.

- **Workload E: Short ranges**

In this workload, short ranges of records are queried, instead of individual records. Application example: threaded conversations, where each scan is for the posts in a given thread (assumed to be clustered by thread id).

- **Workload F: Read-modify-write**

In this workload, the client will read a record, modify it, and write back the changes. Application example: user database, where user records are read and modified by the user or to record user activity.

