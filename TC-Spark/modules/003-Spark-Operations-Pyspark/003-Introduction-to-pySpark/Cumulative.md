<details><summary>Learning Overview</summary>

After Completing This Module, Learners Will Be Able To:

-   Define PySpark and explain its relationship with Apache Spark
-   Describe the key features of PySpark
-   Identify common PySpark use cases
-   Understand how PySpark supports distributed data processing
-   Create a Spark session
-   Load and inspect datasets using PySpark

</details>

<details><summary> Description </summary>

## What is PySpark?

PySpark is the Python API for Apache Spark.

Apache Spark is an open-source distributed computing framework designed
for large-scale data processing. PySpark allows developers and data
engineers to use Spark's distributed processing capabilities using
Python.

In simple terms:

-   Apache Spark is the distributed engine
-   PySpark is the Python interface to that engine

PySpark enables:

-   Distributed batch processing
-   Real-time data processing
-   Machine learning at scale
-   Large-scale data transformations

Although Spark was originally written in Scala, PySpark makes it
accessible to Python developers, which significantly increased its
adoption in the data engineering and data science communities.

------------------------------------------------------------------------

## Why PySpark?

Modern organizations generate massive volumes of data. Traditional
systems struggle with:

-   Large datasets
-   Complex transformations
-   Real-time analytics
-   Distributed computation

PySpark solves these challenges by:

-   Distributing data across multiple machines
-   Processing data in parallel
-   Supporting in-memory computation
-   Providing high-level APIs for structured data

------------------------------------------------------------------------

## Key Features of PySpark

### 1. Distributed Computing

Data is split into partitions and processed across multiple worker nodes
in a cluster.

### 2. In-Memory Processing

Spark can cache data in memory, reducing disk I/O and improving
performance.

### 3. Real-Time and Batch Processing

Supports both batch workloads and real-time data streaming.

### 4. Integration with Python Ecosystem

Works seamlessly with: - Pandas - NumPy - Machine learning libraries -
Visualization tools

### 5. Multiple APIs

PySpark supports: - RDD API - DataFrame API - SQL API - MLlib (Machine
Learning Library) - Structured Streaming

</details>

<details><summary> Real World Application </summary>

PySpark is widely used across industries for large-scale analytics.

## 1. Travel and Hospitality

Travel platforms use Spark to:

-   Analyze user search patterns
-   Provide personalized hotel and flight recommendations
-   Compare pricing across multiple providers
-   Optimize booking systems

## 2. E-Commerce

Online retailers use PySpark to:

-   Analyze customer behavior
-   Recommend products
-   Detect fraudulent transactions
-   Process millions of transactions daily

## 3. Banking and Finance

Financial institutions use PySpark for:

-   Risk analysis
-   Fraud detection
-   Real-time transaction monitoring
-   Large-scale data aggregation

## 4. Machine Learning at Scale

PySpark MLlib allows:

-   Training machine learning models on massive datasets
-   Distributed model training
-   Feature engineering on large-scale data

</details>

<details><summary> Implementation </summary>

## Step 1: Import Required Libraries

``` python
import pyspark
from pyspark.sql import SparkSession
import pandas as pd
```

------------------------------------------------------------------------

## Step 2: Create a Spark Session

The SparkSession is the entry point for working with DataFrames and SQL
in Spark.

``` python
spark = SparkSession.builder.appName("Spark-Introduction").getOrCreate()
```

Explanation:

-   appName() sets the application name
-   getOrCreate() creates a new Spark session or retrieves an existing
    one

------------------------------------------------------------------------

## Step 3: Loading Dataset into PySpark

To load a dataset into Spark, use the read method.

``` python
df_pyspark = spark.read.csv("Example.csv", header=True, inferSchema=True)
df_pyspark.show()
```

Explanation:

-   header=True treats the first row as column names
-   inferSchema=True automatically detects data types
-   show() displays the data

------------------------------------------------------------------------

## Inspecting Data

``` python
df_pyspark.printSchema()
df_pyspark.columns
df_pyspark.describe().show()
```

These methods help understand the structure and statistics of the
dataset.

</details>

<details><summary> Summary </summary>

-   PySpark is the Python API for Apache Spark
-   It enables distributed and parallel data processing using Python
-   It supports batch processing, real-time streaming, and machine learning
-   SparkSession is the entry point for working with structured data
-   Datasets can be loaded using spark.read methods
-   PySpark is widely used in industries handling large-scale data
</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>