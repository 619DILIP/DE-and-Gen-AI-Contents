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