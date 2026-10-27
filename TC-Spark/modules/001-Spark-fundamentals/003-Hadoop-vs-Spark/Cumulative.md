<details><summary> Learning Objectives </summary>

After completing this module, learners will be able to:

-   Understand the architectural differences between Hadoop and Spark
-   Compare MapReduce and Spark execution models
-   Identify performance differences
-   Understand batch vs streaming capabilities
-   Compare fault tolerance mechanisms
-   Choose appropriate use cases for Hadoop or Spark
-   Understand how Python integrates with Spark

</details>

<details><summary> Description </summary>

Hadoop and Spark are both distributed data processing technologies, but
they are designed differently and serve different purposes in modern
data ecosystems.

Hadoop is a distributed storage and batch processing framework. Spark is
a unified analytics engine built for fast, large-scale data processing.

It is important to note that Spark does not replace Hadoop. Spark often
runs on top of Hadoop infrastructure.

------------------------------------------------------------------------

## Architectural Difference

### Hadoop Ecosystem

Hadoop consists of:

-   HDFS (Distributed Storage)
-   MapReduce (Batch Processing Engine)
-   YARN (Resource Manager)

MapReduce follows a strict Map → Shuffle → Reduce execution model and
writes intermediate results to disk.

------------------------------------------------------------------------

### Apache Spark

Spark is:

-   An in-memory distributed data processing engine
-   DAG-based execution engine
-   A unified platform supporting batch, streaming, ML, and graph
    processing

Spark can run:

-   On Standalone clusters
-   On Hadoop YARN
-   On Kubernetes

------------------------------------------------------------------------

## Speed

### Spark

-   Uses in-memory processing
-   Minimizes disk I/O
-   DAG execution engine
-   Up to 100x faster in memory
-   Up to 10x faster on disk compared to MapReduce

### Hadoop MapReduce

-   Writes intermediate data to disk
-   High disk I/O overhead
-   Slower for iterative workloads

Spark is especially faster for:

-   Machine learning
-   Iterative algorithms
-   Interactive queries

------------------------------------------------------------------------

## Ease of Development

### Spark

-   High-level APIs (DataFrames, SQL, ML pipelines)
-   Supports Python (PySpark), Scala, Java, SQL
-   Less boilerplate code
-   Easier debugging and development

Example (PySpark):

``` python
df.groupBy("department").avg("salary").show()
```

### Hadoop MapReduce

-   Requires manual Map and Reduce implementation
-   Typically written in Java
-   More verbose code
-   Harder to maintain

------------------------------------------------------------------------

## Latency

### Spark

-   Low-latency processing
-   Suitable for interactive analytics
-   Supports near real-time streaming (Structured Streaming)

### Hadoop MapReduce

-   High-latency processing
-   Designed primarily for batch workloads

------------------------------------------------------------------------

## Data Processing Capability

  Capability            Hadoop MapReduce            Spark
  --------------------- --------------------------- -----------------
  Batch Processing      Yes                         Yes
  Real-time Streaming   No (needs external tools)   Yes
  Machine Learning      Limited (Mahout)            Yes (MLlib)
  Graph Processing      No                          Yes (GraphX)
  Interactive SQL       Limited                     Yes (Spark SQL)

------------------------------------------------------------------------

## Fault Tolerance

### Hadoop

-   Fault tolerance via data replication in HDFS
-   Tasks are re-executed if they fail

### Spark

-   Fault tolerance via RDD lineage
-   Recomputes lost partitions automatically
-   Works with HDFS replication when running on Hadoop

Both systems provide strong fault tolerance.

------------------------------------------------------------------------

## Security

### Hadoop

-   Mature security ecosystem (Kerberos, Ranger, etc.)

### Spark

-   Integrates with Hadoop security when deployed on YARN
-   Supports authentication and encryption
-   Security depends on deployment configuration

Spark is not insecure by default. Security depends on how the cluster is
configured.

------------------------------------------------------------------------

## Cost Considerations

### Hadoop

-   More disk-heavy architecture
-   Lower memory requirements
-   Cost-effective for large batch jobs

### Spark

-   Requires more RAM
-   Faster performance may reduce total processing time
-   Often cost-effective for advanced analytics workloads

Cost depends on workload type, not just technology choice.

------------------------------------------------------------------------

## Scheduler and Resource Management

### Hadoop MapReduce

-   Relies on YARN for resource management
-   Often uses external schedulers like Oozie

### Spark

-   Has internal task scheduling
-   Can run on YARN, Standalone, or Kubernetes
-   Optimizes task execution via DAG scheduler

------------------------------------------------------------------------

## Language Support

  Platform           Primary Language   Additional Support
  ------------------ ------------------ -------------------------------
  Hadoop MapReduce   Java               Limited streaming integration
  Spark              Scala              Python, Java, SQL

Spark is widely adopted in Python-based data engineering workflows.

</details>

<details><summary> Real World Applications </summary>

### Hadoop Use Cases

-   Large-scale archival data storage
-   Massive batch ETL processing
-   Log storage and historical analysis

Industries using Hadoop:

-   Telecommunications
-   Retail
-   Financial services

------------------------------------------------------------------------

### Spark Use Cases

-   Real-time fraud detection
-   Recommendation engines
-   Machine learning pipelines
-   Streaming analytics
-   Interactive dashboards

Industries using Spark:

-   Banking and finance
-   Healthcare analytics
-   E-commerce platforms
-   Media streaming services

------------------------------------------------------------------------

## When to Choose What?

Choose Hadoop MapReduce when:

-   Processing extremely large batch datasets
-   Budget constraints limit RAM usage
-   Workloads are not latency-sensitive

Choose Spark when:

-   Low latency is required
-   Machine learning is involved
-   Real-time analytics is needed
-   Python-based data engineering is preferred

</details>

<details><summary> Implementation </summary>

### 1. Hadoop MapReduce Example (Conceptual Flow)

In Hadoop MapReduce, developers write:

-   Mapper class
-   Reducer class
-   Driver class

Example (Word Count Logic -- Conceptual):

Mapper: - Input: Line of text - Output: (word, 1)

Reducer: - Input: (word, list_of_counts) - Output: (word, total_count)

Execution Flow: 1. Data stored in HDFS 2. Map phase processes input
splits 3. Shuffle and sort 4. Reduce phase aggregates results 5. Output
written back to HDFS

This requires significant boilerplate code, typically written in Java.

------------------------------------------------------------------------

### 2. Spark Implementation Example (PySpark)

Install PySpark:

``` bash
pip install pyspark
```

Create Spark Session:

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("HadoopVsSparkDemo").getOrCreate()
```

Load Data:

``` python
df = spark.read.text("input.txt")
df.show()
```

Word Count Using Spark:

``` python
from pyspark.sql.functions import explode, split

words = df.select(explode(split(df.value, " ")).alias("word"))

word_counts = words.groupBy("word").count()

word_counts.show()
```

Notice:

-   No manual Map or Reduce functions
-   Minimal code
-   High-level DataFrame API
-   Optimized execution through DAG scheduler

------------------------------------------------------------------------

### 3. Performance Comparison (Practical Understanding)

Hadoop: - Writes intermediate results to disk - Slower for iterative
algorithms

Spark: - Stores intermediate data in memory - Faster for machine
learning and repeated computations

Example Iterative Logic:

``` python
for i in range(5):
    df = df.withColumn("new_col", df.some_column * 2)
```

Spark handles this efficiently due to in-memory processing.

------------------------------------------------------------------------

### 4. Streaming Example (Spark Only)

``` python
stream_df = spark.readStream.format("csv")     .option("header", "true")     .load("stream_folder")

query = stream_df.writeStream     .outputMode("append")     .format("console")     .start()

query.awaitTermination()
```

Hadoop MapReduce does not natively support this.

</details>

<details><summary> Summary </summary>

Hadoop and Spark are complementary technologies in the big data
ecosystem.

Key differences:

-   Hadoop MapReduce is disk-based and batch-oriented.
-   Spark is memory-optimized and supports multiple workloads.
-   Spark provides higher-level APIs and better developer productivity.
-   Both provide fault tolerance and scalability.
-   Spark integrates seamlessly with Python through PySpark.

In modern architectures, Spark often runs on Hadoop infrastructure,
combining HDFS storage with Spark's fast processing capabilities.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>