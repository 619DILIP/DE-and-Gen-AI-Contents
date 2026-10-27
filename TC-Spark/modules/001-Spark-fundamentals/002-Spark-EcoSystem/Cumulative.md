<details><summary> Learning Objectives </summary>

After completing this module, learners will be able to:

-   Understand the components of the Apache Spark Ecosystem
-   Explain the role of Spark Core
-   Work with Spark SQL and DataFrames
-   Understand Structured Streaming concepts
-   Identify use cases of MLlib
-   Understand graph processing with GraphX
-   Use PySpark to interact with Spark ecosystem components

</details>

<details><summary> Description </summary>

Apache Spark is not just a processing engine. It is a unified analytics
platform composed of tightly integrated modules built on top of Spark
Core.

At the center of the ecosystem is Spark Core, which handles distributed
execution, memory management, scheduling, and fault tolerance. Other
components extend this core engine to support SQL, streaming, machine
learning, and graph analytics.

------------------------------------------------------------------------

## Spark Ecosystem Components

![Spark Ecosystem Architecture](Images/Ecosystem.png)

### 1. Apache Spark Core

Spark Core is the foundational execution engine of Spark. All other
components are built on top of it.

Responsibilities:

-   Task scheduling and execution
-   Memory management
-   Fault recovery using RDD lineage
-   Interaction with storage systems (HDFS, S3, etc.)
-   Distributed data processing

RDD (Resilient Distributed Dataset) is the basic abstraction in Spark
Core. It represents an immutable distributed collection of objects.

Key Features:

-   Distributed processing
-   Fault tolerance
-   In-memory computation
-   Lazy evaluation

------------------------------------------------------------------------

### 2. Apache Spark SQL

Spark SQL provides structured data processing using DataFrames and SQL
queries.

Modern Spark uses DataFrames and Datasets instead of the older SchemaRDD
abstraction.

Features:

-   SQL query execution
-   Catalyst optimizer (cost-based query optimizer)
-   Tungsten execution engine for performance optimization
-   Integration with multiple data sources (CSV, JSON, Parquet, ORC,
    Hive)

Example using PySpark:

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("SparkSQL").getOrCreate()

df = spark.read.csv("data.csv", header=True, inferSchema=True)
df.createOrReplaceTempView("students")

spark.sql("SELECT * FROM students WHERE marks > 90").show()
```

------------------------------------------------------------------------

### 3. Structured Streaming (Modern Spark Streaming)

Structured Streaming is the modern streaming engine built on Spark SQL.

It treats streaming data as an unbounded table and applies incremental
processing.

Key Features:

-   Exactly-once processing guarantees
-   Unified batch and streaming APIs
-   Integration with Kafka and other streaming systems
-   Fault-tolerant streaming

Example:

``` python
stream_df = spark.readStream.format("csv").option("header", "true").schema(df.schema).load("streaming_folder")

query = stream_df.writeStream.outputMode("append").format("console").start()

query.awaitTermination()
```

Applications:

-   Real-time fraud detection
-   IoT data processing
-   Log analytics
-   Live dashboards

------------------------------------------------------------------------

### 4. Apache Spark MLlib

MLlib is Spark's distributed machine learning library.

It provides scalable implementations of common algorithms.

Supported algorithms:

-   Classification
-   Regression
-   Clustering
-   Recommendation systems
-   Dimensionality reduction

Example:

``` python
from pyspark.ml.classification import LogisticRegression
from pyspark.ml.feature import VectorAssembler

assembler = VectorAssembler(inputCols=["feature1", "feature2"], outputCol="features")
data = assembler.transform(df)

lr = LogisticRegression(featuresCol="features", labelCol="label")
model = lr.fit(data)
```

MLlib is designed for distributed training and large-scale machine
learning workflows.

------------------------------------------------------------------------

### 5. GraphX

GraphX is Spark's graph processing framework (primarily Scala-based).

It allows graph-parallel computation such as:

-   PageRank
-   Connected components
-   Shortest path algorithms

Graph processing is useful for:

-   Social networks
-   Fraud detection networks
-   Recommendation systems
-   Network topology analysis

Note: GraphX is more commonly used in Scala environments. Python users
typically use GraphFrames as an alternative.

</details>

<details><summary> Real World Applications </summary>

### eBay

eBay uses Spark for targeted recommendations, customer personalization,
and performance optimization. Spark runs on Hadoop YARN clusters with
thousands of nodes to process massive datasets.

### Netflix

Netflix uses Spark for:

-   Real-time streaming analytics
-   Recommendation systems
-   Event processing pipelines

Billions of daily events are processed using Spark integrated with
Kafka.

### Banking and Finance

-   Fraud detection systems
-   Risk analytics
-   Real-time transaction monitoring

### Healthcare

-   Patient analytics
-   Disease trend prediction
-   Research data processing

### E-commerce

-   Customer behavior analysis
-   Real-time recommendations
-   Inventory optimization

</details>

<details><summary> Implementation </summary>

Below is a simple end-to-end ecosystem example:

``` python
from pyspark.sql import SparkSession
from pyspark.ml.feature import VectorAssembler
from pyspark.ml.clustering import KMeans

spark = SparkSession.builder.appName("SparkEcosystemDemo").getOrCreate()

# Load data
df = spark.read.csv("data.csv", header=True, inferSchema=True)

# SQL query
df.createOrReplaceTempView("data_table")
spark.sql("SELECT * FROM data_table LIMIT 5").show()

# ML example
assembler = VectorAssembler(inputCols=["feature1", "feature2"], outputCol="features")
data = assembler.transform(df)

kmeans = KMeans(k=2, seed=1)
model = kmeans.fit(data)

# Show cluster centers
print(model.clusterCenters())
```

This demonstrates integration of Spark SQL and MLlib within one unified
engine.

</details>

<details><summary> Summary </summary>

The Spark Ecosystem is a unified analytics platform built around Spark
Core.

Key components:

-   Spark Core → Distributed execution engine
-   Spark SQL → Structured data processing
-   Structured Streaming → Real-time data processing
-   MLlib → Machine learning library
-   GraphX → Graph analytics

Spark provides a single platform for:

-   Batch processing
-   Streaming analytics
-   Machine learning
-   Graph computation

With PySpark, Python developers can leverage the full Spark ecosystem to
build scalable, production-grade data engineering and data science
pipelines.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>