---
title: "HiBench: a Big Data Benchmark Suite"
date: 2020-12-01T20:51:41+08:00
image: 'p5.jpg'
---

## HiBench Overview

HiBench is a big data benchmark suite that helps evaluate different big data frameworks in terms of speed, throughput and system resource utilizations. It contains a set of Hadoop, Spark and streaming workloads, including Sort, WordCount, TeraSort, Repartition, Sleep, SQL, PageRank, Nutch indexing, Bayes, Kmeans, NWeight and enhanced DFSIO, etc. It also contains several streaming workloads for Spark Streaming, Flink, Storm and Gearpump.



### Micro Benchmarks

These benchmarks consist of a few micro tasks for Hadoop to perform, which requires less resource and relatively faster to execute.

- Sort

This workload sorts its *text* input data, which is generated using RandomTextWriter.

- WordCount

This workload counts the occurrence of each word in the input data, which are generated using RandomTextWriter. It is representative of another typical class of real world MapReduce jobs - extracting a small amount of interesting data from large data set.

- TeraSort

TeraSort is a standard benchmark created by Jim Gray. Its input data is generated by Hadoop TeraGen example program.



### Machine Learning Benchmarks

These benchmarks consist of a few popular machine learning algorithm implemented in Hadoop MapReduce and Apache Spark.

- Bayesian Classification

Naive Bayes is a simple multiclass classification algorithm with the assumption of independence between every pair of features. This workload is implemented in spark.mllib and uses the automatically generated documents whose words follow the zipfian distribution. The dict used for text generation is also from the default linux file /usr/share/dict/linux.words.ords.

- K-means clustering

This workload tests the K-means (a well-known clustering algorithm for knowledge discovery and data mining) clustering in spark.mllib. The input data set is generated by GenKMeansDataset based on Uniform Distribution and Guassian Distribution. There is also an optimized K-means implementation based on DAL (Intel Data Analytics Library), which is available in the dal module of sparkbench.



### SQL Benchmarks

- Scan, Join and Aggregate

These workloads are developed based on SIGMOD 09 paper "A Comparison of Approaches to Large-Scale Data Analysis" and HIVE-396. It contains Hive queries (Aggregation and Join) performing the typical OLAP queries described in the paper. Its input is also automatically generated Web data with hyperlinks following the Zipfian distribution.



### Websearch Benchmarks

- PageRank

This workload benchmarks PageRank algorithm implemented in Spark-MLLib/Hadoop (a search engine ranking benchmark included in pegasus 2.0) examples. The data source is generated from Web data whose hyperlinks follow the Zipfian distribution.

