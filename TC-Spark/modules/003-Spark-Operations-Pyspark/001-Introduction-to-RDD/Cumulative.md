<details><summary>Learning Overview</summary>

After Completing This Module, You Will Be Able To:

-   Define RDD and explain why it was introduced in Apache Spark
-   Describe the internal working principles of RDDs
-   Explain immutability and why it matters in distributed systems
-   Understand lineage and how Spark achieves fault tolerance
-   Differentiate between transformations and actions
-   Explain how lazy evaluation improves performance
-   Understand partitions and their impact on parallelism
-   Create RDDs using multiple approaches in PySpark
-   Apply RDD concepts to practical real-world big data scenarios

</details>

<details><summary>Description</summary>

## What is an RDD?

RDD stands for **Resilient Distributed Dataset**.

An RDD is:

-   A distributed collection of data
-   Divided into logical partitions
-   Stored across multiple nodes in a cluster
-   Processed in parallel
-   Fault tolerant through lineage tracking
-   Immutable once created

RDD is the lowest-level data abstraction in Spark. Although Spark now
provides DataFrames and Datasets, those abstractions are internally
built on RDDs.

Understanding RDDs helps learners understand how Spark executes
distributed computations under the hood.

------------------------------------------------------------------------

## Why RDD Was Introduced

Before Spark, Hadoop MapReduce dominated big data processing. However:

-   MapReduce writes intermediate results to disk after every stage
-   Iterative algorithms become slow due to repeated disk I/O
-   Interactive analytics becomes inefficient

Spark introduced RDDs to enable:

-   In-memory computation
-   Efficient iterative processing
-   Reduced disk I/O
-   Faster performance for analytics and machine learning

------------------------------------------------------------------------

## Core Characteristics of RDD

### 1. Immutable

Once an RDD is created, it cannot be modified.

Instead of modifying data: - Transformations create a new RDD - Original
RDD remains unchanged

This design ensures safe parallel execution and prevents concurrency
issues.

Example:

``` python
rdd2 = rdd1.map(lambda x: x * 2)
```

------------------------------------------------------------------------

### 2. Resilient (Fault Tolerant)

RDDs track transformations in a lineage graph (Directed Acyclic Graph -
DAG).

If a node fails: - Spark identifies the lost partition - Uses lineage to
recompute only that partition - Avoids recomputing the entire dataset

This eliminates the need for expensive data replication.

------------------------------------------------------------------------

### 3. Lazy Evaluation

Transformations are not executed immediately.

Spark builds an execution plan and only executes it when an action is
triggered.

Benefits: - Optimized execution plan - Reduced redundant computation -
Efficient resource utilization

Example:

Transformation:

``` python
rdd2 = rdd1.map(lambda x: x + 1)
```

Action:

``` python
rdd2.collect()
```

Execution happens only when `collect()` is called.

![RDD](Images/RDD.PNG)

------------------------------------------------------------------------

### 4. Distributed

RDDs are partitioned across worker nodes.

Each partition: - Is processed by one task - Runs independently -
Contributes to parallelism

Number of partitions directly affects performance.

------------------------------------------------------------------------

### 5. Persistence and Caching

RDDs can be stored in:

-   MEMORY_ONLY
-   MEMORY_AND_DISK
-   DISK_ONLY

Example:

``` python
rdd.cache()
```

Caching is useful in iterative workloads where the same RDD is reused
multiple times.

</details>

<details><summary>Real World Application</summary>

RDDs are particularly useful in the following scenarios:

## 1. Log Processing

Web servers generate large log files. RDDs can:

-   Distribute log files across cluster nodes
-   Extract error messages
-   Count status codes
-   Identify frequent IP addresses

## 2. ETL (Extract Transform Load) Pipelines

RDDs can: - Read raw files - Filter invalid records - Transform data
formats - Aggregate metrics - Load processed data into storage

## 3. Machine Learning Workloads

Iterative algorithms such as gradient descent benefit from in-memory
caching of RDDs to avoid repeated disk reads.

## 4. Batch Data Processing

Organizations processing daily transaction data can use RDDs to:

-   Compute totals
-   Perform aggregations
-   Generate reports
-   Detect anomalies

</details>

<details><summary> Implementation </summary>

## Step 1: Import Required Libraries

``` python
from pyspark import SparkContext, SparkConf
```

## Step 2: Create Spark Configuration and Context

``` python
conf = SparkConf().setMaster("local[*]").setAppName("RDDExample")
sc = SparkContext(conf=conf)
```

Explanation: - local\[\*\] uses all available cores - SparkContext
initializes the Spark execution environment

------------------------------------------------------------------------

## Method 1: Create RDD Using parallelize()

``` python
data = [10, 20, 30, 40, 50]
rdd = sc.parallelize(data)
```

Check partitions:

``` python
rdd.getNumPartitions()
```

------------------------------------------------------------------------

## Method 2: Create RDD from Existing RDD

``` python
rdd1 = sc.parallelize([1, 2, 3])
rdd2 = rdd1.map(lambda x: x + 1)
rdd2.collect()
```

-   map() → Transformation
-   collect() → Action

------------------------------------------------------------------------

## Method 3: Create RDD from External File

``` python
rdd = sc.textFile("data.txt")
```

Each line becomes one element in the RDD.

Common sources: - HDFS - Amazon S3 - Local file system

------------------------------------------------------------------------

## Method 4: Create RDD from DataFrame

``` python
demo_rdd = df.rdd
```

Converts structured data into an RDD of Row objects.

------------------------------------------------------------------------

# Transformations vs Actions

## Transformations (Lazy)

-   map()
-   filter()
-   flatMap()
-   reduceByKey()
-   distinct()

## Actions (Trigger Execution)

-   collect()
-   count()
-   take()
-   first()
-   saveAsTextFile()

Transformations build a DAG; actions execute it.

</details>

<details><summary> Summary </summary>
 
-   RDD is the foundational distributed data abstraction in Apache Spark
-   It is immutable, distributed, fault tolerant, and lazily evaluated
-   Fault tolerance is achieved using lineage instead of data
    replication
-   RDDs support in-memory processing for improved performance
-   Partitioning enables parallel execution
-   RDDs can be created from collections, files, existing RDDs, or
    DataFrames
-   Understanding RDDs is essential for mastering Spark's distributed
    execution model

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>