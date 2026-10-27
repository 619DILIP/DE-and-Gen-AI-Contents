# Cumulative for the Working with RDDs
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites

- Basic knowledge of the Hadoop file system, Python or Scala, or Java programming languages, and the basics of any distributed database.

## Learning Objectives

- After completing this module, anyone will be able to understand RDDs in SparkContext.

</details>
<details><summary>Description</summary>

## Description

**RDD**
  
- The RDD (Resilient Distributed Dataset) is the basic form of data abstraction in Apache Spark and Spark Core. It is a fundamental Spark data structure. As fault-tolerant, immutable distributed groups of objects, RDDs cannot be altered after they have been created. Logical partitions are created for each dataset in RDD so that they can be processed on several cluster nodes.

- Additionally, RDDs provide data abstraction for the distribution of the data and partitioning, which is intended to run computations concurrently across multiple nodes. When performing transformations on RDDs, we typically don't need to worry about parallelism because Spark already offers it by default.

**RDD Creation**

- RDDs are typically created in one of two ways: by parallelizing an existing collection or by referencing a dataset in an external storage system (HDFS, S3, and many more).

</br>

![RDD](Images/rdd.PNG)

</br>

**sparkContext.parallelize()**

- The `sparkContext.parallelize()` method is used to parallelize an existing collection in your driver program and is used to create RDDs.

**sparkContext.textFile()**

- Using the `textFile()` function or method, we can read a text file into RDD.

**sparkContext.wholeTextFiles()**

- The `sparkContext.wholeTextFiles()` function returns a PairRDD with the key being the file path and the value being the file content.

**sparkContext.emptyRDD()**

- Using the `sparkContext.emptyRDD()` method on SparkContext, we can create an RDD with no data, and this method is used to create an empty RDD with no partitions.

**Creating an empty RDD with partitions**

- An empty RDD may sometimes need to be written to files using partitioning; in this case, you should create an empty RDD with partitions.

**RDD Parallelize and repartition**

- When we use `parallelize()`, `textFile()`, or `wholeTextFiles()` methods to launch RDDs, the data is automatically partitioned based on resource availability.

**getNumPartitions** - Returns the number of partitions our dataset was divided into. Any transformations that are applied to an RDD execute concurrently. For each partition of the cluster, Spark will execute a single task.

**Set parallelize manually** - The second parameter of these operations, such as `sparkContext.parallelize(dataSeq, 10)`, can be used to explicitly set the number of partitions if needed.

**Repartition using repartition and coalesce** - Spark offers two methods for repartitioning RDDs: the `repartition()` method, also known as full shuffle, which shuffles data from all nodes, and the `coalesce()` method, which shuffles data from the minimum number of nodes. For example, if your data is divided into four partitions, `coalesce(2)` will only move data from two nodes.

**RDD Advantages**

- In-Memory Processing   
- Immutability   
- Fault Tolerance   
- Lazy Evaluation   
- Partitioning   
- Parallelization   
</details>
<details><summary>Real World Application</summary>

</details>
<details><summary>Implementation</summary> 

## Implementation

**RDD Creation**

- RDDs are typically created in one of two ways: by parallelizing an existing collection or by referencing a dataset in an external storage system (HDFS, S3, and many more).

```scala
val spark: SparkSession = SparkSession.builder()
      .master("local[1]")
      .appName("SparkByExamples.com")
      .getOrCreate()    
```

</br>

![RDD](Images/rdd.PNG)

</br>

**sparkContext.parallelize()**

- The `sparkContext.parallelize()` method is used to parallelize an existing collection in your driver program and is used to create RDDs.

```scala
val dataSeq = Seq(("Java", 20000), ("Python", 100000), ("Scala", 3000))   
val rdd = spark.sparkContext.parallelize(dataSeq)
```

**sparkContext.textFile()**

- Using the `textFile()` function or method, we can read a text file into RDD.

```scala
val rdd2 = spark.sparkContext.textFile("/path/textFile.txt")
```

**sparkContext.wholeTextFiles()**

- The `sparkContext.wholeTextFiles()` function returns a PairRDD with the key being the file path and the value being the file content.
  
```scala
val rdd3 = spark.sparkContext.wholeTextFiles("/path/textFile.txt")
```

**sparkContext.emptyRDD()**

- Using the `sparkContext.emptyRDD()` method on SparkContext, we can create an RDD with no data, and this method is used to create an empty RDD with no partitions.

```scala
val rdd = spark.sparkContext.emptyRDD 
val rddString = spark.sparkContext.emptyRDD[String] 
```

**Creating an empty RDD with partitions**

- An empty RDD may sometimes need to be written to files using partitioning; in this case, you should create an empty RDD with partitions.

```scala
val rdd2 = spark.sparkContext.parallelize(Seq.empty[String])
```

**RDD Parallelize and repartition**

- When we use `parallelize()`, `textFile()`, or `wholeTextFiles()` methods to launch RDDs, the data is automatically partitioned based on resource availability.

**getNumPartitions** - Returns the number of partitions our dataset was divided into. Any transformations that are applied to an RDD execute concurrently. For each partition of the cluster, Spark will execute a single task.

```scala
println("initial partition count: " + rdd.getNumPartitions)
```

**Set parallelize manually** - The second parameter of these operations, such as `sparkContext.parallelize(dataSeq, 10)`, can be used to explicitly set the number of partitions if needed.

**Repartition using repartition and coalesce** - Spark offers two methods for repartitioning RDDs: the `repartition()` method, also known as full shuffle, which shuffles data from all nodes, and the `coalesce()` method, which shuffles data from the minimum number of nodes. For example, if your data is divided into four partitions, `coalesce(2)` will only move data from two nodes.

```scala
val reparRdd = rdd.repartition(4)
println("re-partition count: " + reparRdd.getNumPartitions)
```

- `repartition()` or `coalesce()` methods also return a new RDD.
</details>
<details><summary>Summary</summary> 

## Summary

- In the above module, we have learned that the RDD (Resilient Distributed Dataset) is the basic form of data abstraction in Apache Spark and Spark Core. It is a fundamental Spark data structure. As fault-tolerant, immutable distributed groups of objects, RDDs cannot be altered after they have been created. Logical partitions are created for each dataset in RDD so that they can be processed on several cluster nodes.

**RDD Creation**

- RDDs are typically created in one of two ways: by parallelizing an existing collection or by referencing a dataset in an external storage system (HDFS, S3, and many more).

```scala
val spark: SparkSession = SparkSession.builder()
      .master("local[1]")
      .appName("SparkByExamples.com")
      .getOrCreate()    
```

</br>

![RDD](Images/rdd.PNG)

</br>

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
