# Cumulative for the Introduction to RDD
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites 

- Programming experience in Python or Scala. 

## Objectives

- To understand the core concepts of RDDs in Spark and their usage.

---

</details>
<details><summary>Description</summary>

## Description

- RDDs are the core of Apache Spark. It stands for Resilient Distributed Datasets. This is a data structure that has been present since the initial release of Spark. Now, along with RDDs, DataFrames and Datasets have been introduced in newer versions of Spark that are built on top of RDDs. 

- Anything you do in Spark revolves around the RDD, and each RDD is distributed across different nodes of the cluster in a production scenario. RDDs are stored in RAM and not on a hard disk, which makes Spark processing faster than any other application. 

![RDD](Images/RDD.PNG)

## Features of RDD in Spark

- **Immutable:** RDDs are immutable collections of objects, meaning we cannot change the state of an RDD. Instead, we can create another RDD from its previous RDD by applying different operations. 

- **Resilient:** RDDs are resilient, meaning they provide fault tolerance. Each transformation operation applied to RDDs is stored in a lineage graph, which helps in recomputing any damaged or missing partition due to node failure.

- **Lazy Evaluation:** Transformation operations applied to RDDs are executed only when an action is triggered. These RDDs are not evaluated until a result is needed, which makes their evaluation lazy and thus increases the performance of an application.

- **Distributed:** RDD data is distributed across multiple nodes of a cluster, which makes the data highly available. 

- **Persistence:** Intermediate results of RDDs can be reused by users, and they can select their storage location as well, either in memory or on disk, for fast computations. 

## Ways of Creating RDD

- It can be created by using the `parallelize()` method. 
- It can be created from an existing RDD. 
- It can be created from external storage like HDFS, Amazon S3, HBase, etc. 
- It can be created from existing DataFrames and Datasets. 

---

</details>


<details><summary>Implementation</summary> 

## Implementation

As we have already discussed the several ways of creating an RDD in Spark, let us now see how to create them. 

**1. Creating an RDD using the `parallelize()` method**

- To create an RDD, first, we must import Spark classes.

```
import org.apache.spark.SparkContext
import org.apache.spark.SparkConf
```

- Then create `SparkConf` and `SparkContext` objects.

```
val conf = new SparkConf().setMaster(master).setAppName(app_name)

val sc = new SparkContext(conf) 

```
**Note:** 
> `setMaster()` and `setAppName()` are the minimum properties required to run a Spark application.

- Now, we can use `parallelize()` with three types of collections: array, sequence, and list. We will see each one in turn. 
  - **Creating RDD from an Array Collection**
  ```
  val data = Array(1,2,3,4,5)
  val arr_rdd = sc.parallelize(data)
  ```

  - **Creating RDD from a Sequence Collection**
  ```
  val data = Seq(1,2,3,4,5)
  val sequence_rdd = sc.parallelize(data)
  ```

  - **Creating RDD from a List Collection**
  ```
  val data = List(1,2,3,4,5)
  val list_rdd = sc.parallelize(data)
  ```

- The purpose of `parallelize()` is to distribute the data from the specified collection across multiple nodes of a cluster so that data processing can occur in parallel, resulting in faster outcomes. 


**2. Creating RDD from an Existing RDD**

- When we apply any transformation operation on an existing RDD, a new RDD is created. For example, we will apply the `map()` function to the existing RDD "rdd1".
```
val rdd1 = sc.parallelize(Array(1, 2, 3)) 

val rdd2 = rdd1.map(sum => sum + 1)
rdd2.collect
```

- Here, `collect` is an action applied to `rdd2` to retrieve all the elements on the output screen.

**Note:**
> We will discuss more about RDD operations in the Basic-RDD-Operations module. 


**3. Creating RDD from an Existing DataFrame or Dataset** 

- To convert any DataFrame or Dataset to an RDD, simply add `rdd` to it. For example, let's assume we have a DataFrame called "df" and we want to convert it into an RDD. To do this, we must write...
```
val demo_rdd = df.rdd
```

**Note:** 
> In the "Data-Load-Store" module, we will see how to create an RDD from a referenced dataset.

---

</details>
<details><summary>Summary</summary> 

## Summary

- RDDs are the fundamental data structures of Spark that are logically partitioned across different nodes of a cluster. Each RDD partition can be stored and processed on different nodes. 

- They are immutable collections of objects that are distributed and fault-tolerant in nature. 

- Spark RDDs can be created in different ways: by using the `parallelize()` method, by applying transformation operations on existing RDDs, or by converting DataFrames or Datasets using the `rdd` property, etc. 

---

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
