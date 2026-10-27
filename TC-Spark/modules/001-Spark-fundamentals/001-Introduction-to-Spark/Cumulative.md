<details><summary> Learning Objectives </summary>

After completing this module, learners will be able to:

-   Explain what Apache Spark is and why it is used
-   Differentiate Spark from Hadoop MapReduce
-   Understand Spark architecture and execution model
-   Describe Spark deployment modes
-   Understand Spark ecosystem components
-   Create and manipulate DataFrames using PySpark
-   Identify real-world applications of Spark

</details>

<details><summary> Description </summary>

### History of Apache Spark

Apache Spark was initiated in 2009 by Matei Zaharia at UC Berkeley's
AMPLab to overcome performance limitations of Hadoop MapReduce. It was
open-sourced in 2010 and donated to the Apache Software Foundation in 2013. In 2014, Spark became a top-level Apache project.

Today, Spark is one of the most widely adopted distributed processing
engines in data engineering and data science ecosystems.

------------------------------------------------------------------------

### What is Apache Spark?

Apache Spark is a distributed, in-memory data processing engine designed
for large-scale data analytics. Unlike Hadoop MapReduce, which writes
intermediate results to disk, Spark keeps data in memory whenever
possible, significantly improving performance.

Spark supports:

-   Batch data processing
-   Interactive SQL queries
-   Real-time data processing (Structured Streaming)
-   Machine learning
-   Graph processing

Spark is not a replacement for Hadoop but can run on Hadoop clusters or
independently.

------------------------------------------------------------------------

### Why Spark?

Hadoop MapReduce processes data in strict Map → Shuffle → Reduce stages
and frequently writes intermediate results to disk. This increases
latency.

Spark improves performance through:

-   In-memory computation
-   Directed Acyclic Graph (DAG) execution engine
-   Reduced disk I/O
-   Lazy evaluation of transformations

Performance benefits:

-   Up to 100x faster in memory
-   Up to 10x faster on disk compared to MapReduce

Spark also supports multiple programming languages including Python
(PySpark), Scala, Java, and SQL.

------------------------------------------------------------------------

### Key Features of Apache Spark

-   In-memory distributed processing
-   Fault tolerance via RDD lineage
-   Lazy evaluation
-   DAG-based execution engine
-   Scalable cluster architecture
-   Multi-language API support
-   Unified analytics platform
-   Real-time and batch processing capabilities

------------------------------------------------------------------------

### Spark Architecture

Spark architecture includes:

1.  Driver Program
    -   Entry point of the Spark application
    -   Creates SparkSession
    -   Converts user code into tasks
2.  Cluster Manager
    -   Allocates resources
    -   Can be Standalone, YARN, or Kubernetes
3.  Worker Nodes
    -   Execute assigned tasks
4.  Executors
    -   Run tasks on worker nodes
    -   Store intermediate data

Spark uses a DAG scheduler instead of traditional MapReduce stages,
enabling optimized execution plans.

------------------------------------------------------------------------

### Spark Deployment Modes

![Spark](Images/spark.PNG)

1.  Standalone Mode
    -   Spark's built-in cluster manager
    -   Suitable for small to medium clusters
2.  Hadoop YARN
    -   Spark runs within Hadoop ecosystem
    -   Shares cluster resources
3.  Kubernetes
    -   Containerized Spark deployment
    -   Common in cloud-native environments

Note: Spark in MapReduce (SIMR) is outdated and rarely used in modern
architectures.

------------------------------------------------------------------------

### Spark Ecosystem Components

-   Spark Core → Fundamental distributed processing
-   Spark SQL → Structured data and SQL queries
-   Structured Streaming → Real-time stream processing
-   MLlib → Machine learning library
-   GraphX → Graph computation engine


</details>

<details><summary> Real World Application </summary>

Apache Spark is widely used across industries for large-scale analytics
and machine learning.

### Banking and Finance

-   Fraud detection
-   Risk modeling
-   Real-time transaction analysis
-   Investment pattern recognition

### Healthcare

-   Patient data processing
-   Disease trend analytics
-   Medical research insights

### E-commerce

-   Recommendation engines
-   Customer behavior analytics
-   Real-time personalization
-   Inventory forecasting

### Media and Streaming Platforms

-   Log analytics
-   Engagement tracking
-   Real-time content optimization

### Machine Learning Pipelines

-   Distributed feature engineering
-   Model training on massive datasets
-   Scalable data preprocessing

Spark is especially valuable when organizations need fast processing
over massive distributed datasets.

</details>

<details><summary> Implementation </summary>

### Installing PySpark

``` bash
pip install pyspark
```

------------------------------------------------------------------------

### Creating a Spark Session

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder     .appName("SparkIntroduction")     .getOrCreate()
```

------------------------------------------------------------------------

### Creating a DataFrame

``` python
data = [
    ("Daniel", 95),
    ("Akshat", 96),
    ("Andrew", 90)
]

columns = ["Name", "Marks"]

df = spark.createDataFrame(data, columns)
df.show()
```

------------------------------------------------------------------------

### Filtering Data

``` python
df.filter(df.Marks > 90).show()
```

------------------------------------------------------------------------

### Aggregation Example

``` python
df.groupBy().avg("Marks").show()
```

------------------------------------------------------------------------

### Reading Data from CSV

``` python
df = spark.read.csv("data.csv", header=True, inferSchema=True)
df.printSchema()
df.show()
```

------------------------------------------------------------------------

### Writing Data

``` python
df.write.mode("overwrite").csv("output_folder")
```

------------------------------------------------------------------------

### Understanding Lazy Evaluation

Transformations such as:

-   filter()
-   select()
-   groupBy()

are not executed immediately. Spark executes them only when an action
like:

-   show()
-   collect()
-   count()

is triggered.

</details>

<details><summary> Summary </summary>

Apache Spark is a powerful distributed data processing engine built for
high-performance analytics at scale.

Key takeaways:

-   Spark performs in-memory distributed computation.
-   It uses DAG-based execution instead of strict MapReduce.
-   It supports batch processing, streaming, machine learning, and graph analytics.
-   It can be deployed in Standalone, YARN, or Kubernetes environments.
-   PySpark enables Python developers to build scalable data engineering and machine learning pipelines.

Spark remains a foundational technology in modern data engineering,
real-time analytics, and large-scale machine learning workflows.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>