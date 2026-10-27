## Description

- RDDs are the core of Apache Spark. It stands for Resilient Distributed Datasets. This is a data structure that is present from the initial release of spark. Now along with RDDs, dataframes and Datasets have been introduced in the newer versions of spark that are built on the top of RDD. 

- Anything in Spark you do revolves around the RDD and each RDD is distributed across different nodes of the cluster in the production scenario. RDDs are stored in RAM and not in Hard Disk which makes spark processing faster than any other application. 

![RDD](Images/RDD.PNG)

## Features of RDD in Spark

- **Immutable:** RDDs are immutable collection of objects, Meaning we cannot change the state of RDD, instead we can create another RDD from its previous RDD by applying different operations. 

- **Resilient:** RDDs are resilient, meaning they provide fault tolerance. Each transformation operation applied on RDDs are stored in lineage graph which helps in recompute any damaged or missing partition because of node failure.

- **Lazy Evaluation:** Transformation operations applied on RDDs are executed only when any action is triggered. These RDDs are not evaluated until any result is needed which makes its evaluation lazy and thus increased the performance of an application.

- **Distributed:** RDD data is being distributed on multiple nodes of a cluster. Which makes its data high available. 

- **Persistence:** Intermediate results of RDD can be reused by users and they can select their storage location as well, either in-memory or in disk, for fast computations. 


## Ways of Creating RDD

- It can be created by using parallelize() method. 
- It can be created from existing RDD. 
- It can be created from external storage like HDFS, Amazon S3, HBase, etc. 
- It can be created from existing Dataframe and Dataset. 

---

