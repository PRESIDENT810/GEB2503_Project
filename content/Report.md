---
title: "Report"
date: 2020-12-06T19:39:49+08:00
---

## BigAgriculture: A Smart Farming System Supported By Big Data Infrastructures

Kaining Zhong

The Chinese University of Hong Kong, Shenzhen

117010420@link.cuhk.edu.cn



### Abstraction

Traditional agriculture is facing many challenges in order to adapt to the growing scale of farming. For example, when the size of planting is huge, it is impractical for farmers to know the specific detail of each part of their land; therefore, it is difficult to improve the precision of farming. With big data and Internet of Things (IoT) device, it becomes possible for farmers to know the condition precisely, and fertilize the lands according to their condition. With technologies like GPS and sensors, farmers are able to monitor the temperature, light, humidity condition at all times; thus reduce labor and cost. In this paper, we proposed a smart farming system that can benefit farmers to monitor the environment, and make predictions about the pest, output. By utilizing the power of data science, various machine learning algorithms can be applied to smart agriculture, and improve the overall efficiency of farming.



### Overview of BigAgriculture

To give a brief overview of our BigAgriculture system, we first need to define what is smart farming, and then argue how our BigAgriculture system facilitate its operation. According the description in *Scientific development of smart farming technologies and their application in Brazil* (D. Pivoto), smart farming is based on the incorporation of information and communication technologies into machinery, equipment, and sensors in agricultural production systems. It allows a large volume of data and information to be generated with progressive insertion of automation into the process. To better serve smart farming, we proposed BigAgriculture, an aggregated system for smart farming. BigAgriculture allows farmers to conveniently get access to environmental information of their land, and give prediction about the output of their farm, the severity of pest, etc. using machine learning algorithms. In addition, we also provides visualization of these results, which gives farmers an intuitive understanding about how the situation is. There are a few major components of BigAgriculture:

- Sensor

Sensor is an important link in IoT infrastructure, where it can detect various factors of environments nearby, such as temperature, light, humidity. It can also detect the chemical materials in soils. By connecting to LAN of WAN, sensors are able to send data to a central server, which is often on the cloud.

- Software

Software is used to collect informations provided by sensors, and do the analysis as well as visualization. For BigAgriculture system, we decide to use open source programs. For big data application, we use Apache Hadoop as our distributed system to store data sent by sensors. Since the amount of data is significantly large, it is impractical to store all the   on a single device, and this is why we want to use distributed system. For data analysis, we use Tensorflow to do the prediction, which is a very popular deep learning framework that enable us to implement various machine learning algorithms. As for visualization, we use Python's matplotlib and seaborn library.

- Connectivity

To allow our sensors to send data to our cloud servers, we decide to use LoRa as our communication network. The reason why we are using LoRa is because it can cover range of a few kilometers, which is greater than cellular network. It is also designed for devices that require low power and low cost. In BigAgriculture system, we would like to provide convenience to farmers as much as possible, and we do not want them to replace battery of our IoT sensors frequently. Therefore, LoRa becomes our first choice for communication network. In addition, considering the farm often being a very large area, the advantage that LoRa is able to transmit data over a wide area also benefits a lot to our BigAgriculture system.



### Optimization Problem for Data Transmission

The main problem for data transmission is that each sensor transmit its data to the central server using LoRa, whereas a sensor standing right next to the central server can easily overwhelm another sensor far away at the edge of the cell. This is called Near Far Problem. To solve this problem, we use Linear Programming to solve this problem.

We define

$$SIR_i=\frac{G_{ii}p_i}{\sum_{i\ne j}G_{ij}p_j+n_i}$$

Where G is the channel gain, and p is the power.

Our objective is to minimize the overall power usage, while ensure signal intensity received for each sensor is above its minimum threshold:

$$ min \sum_i p_i $$

$$ subject\ to\ SIR_i(p) \ge \gamma_i, \forall\ i $$

This is a linear programming problem, and we can solve it with optimization algorithms.



### Big Data Infrastructure for BigAgriculture

To better manipulate huge data collected by sensors, we need a realible distributed system to store these data and do the computation. Apache Hadoop is a very popular distributed system framework, and provides many useful components, such as HDFS, MapReduce and HBase.

The Hadoop Distributed File System (HDFS) is part of the Apache Hadoop Core project. It is a distributed file system designed to run on commodity hardware. It has many similarities with existing distributed file systems. However, the differences from other distributed file systems are significant. HDFS is highly fault-tolerant and is designed to be deployed on low-cost hardware. HDFS provides high throughput access to application data and is suitable for applications that have large data sets. HDFS relaxes a few POSIX requirements to enable streaming access to file system data.

Hadoop MapReduce is a software framework for easily writing applications which process vast amounts of data (multi-terabyte data-sets) in-parallel on large clusters (thousands of nodes) of commodity hardware in a reliable, fault-tolerant manner.

Apache HBase is used when you need random, realtime read/write access to your Big Data. This project's goal is the hosting of very large tables -- billions of rows with millions of columns -- atop clusters of commodity hardware. Apache HBase is an open-source, distributed, versioned, non-relational database modeled after Google's Bigtable: A Distributed Storage System for Structured Data by Chang et al. Just as Bigtable leverages the distributed data storage provided by the Google File System, Apache HBase provides Bigtable-like capabilities on top of Hadoop and HDFS.

In our BigAgriculture system, Apache Hadoop servers as the overall big data infrastructure. We use HDFS to store huge agriculture data, and use Hadoop MapReduce to aggregate all the data for computation. If we need to query data in realtime, we can use HBase to provide database service. By combining these tools, we can achieve a basic cloud service for big agriculture data, and thus facilitate data analysis and visualization.



### Regression Problem for Prediction

As central server receive environmental information, and then we can use this information to infer the output of the land, and whether it suffers from pests.

Take the example of making prediction of the output, we will use Linear Regression algorithm. Suppose data such as temperature, light, humidity are labeled as the independent variables \(x_1, x_2...x_n\), and the output of the land is the dependent variable \(y\), we can use historical data to train our linear regression model, and then make prediction about the future output. To train our model, we first use Maximum Likelihood Estimation (MLE) to make parameter estimation. Suppose we have \(m\) historical data of independent variables \(x_{11}, x_{12}...x_{1n}\dots\ x_{m1}, x_{m2}...x_{mn}\) denoted by a \(m\times n\) matrix \(X\) and their corresponding dependent variables \(y_1, y_2...y_m\), denoted by a vector \(y\) with length of \(m\). Linear Regression model assume there exists a linear relationship between independent variables and dependent variables: \(y_i=w^Tx_i+\epsilon_i\), where \(\epsilon_i\) follows normal distribution. By MLE, we can estimate \(\hat w=(X^TX)^{-1}X^Ty\), and then we can make predictions.

With various machine learning algorithm, farmers can easily estimate their payoff of farming, and better plan for the future. It is the same for predict whether their land suffers from pests, with Logistic Regression instead of Linear Regression.



### Conclusion

In the era of big data, the importance of utilizing various advanced cloud computing tools becomes more and more critical. By utilizing the power of sensors, open source softwares and communication network, our BigAgriculture system provides one-stop service to collect, store, analyze and visualize agriculture data. By machine learning algorithms's prediction, farmers can grasp a better understanding of their land, without the necessity of actually visiting the field. With our BigAgriculture system, it is undoubted that the efficiency of smart farming will be further improved, and the cost for labor will be considerably reduced.