<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain the purpose of Hadoop in Big Data systems.
- Explain the purpose of HDFS.
- Describe the roles of NameNode and DataNode.
- Explain how files are stored as blocks in HDFS.
- Explain the purpose of data replication and fault tolerance.
- Describe the basic MapReduce processing model.
- Explain the purpose of Apache Spark.
- Explain what PySpark is and how it is used.
- Create and work with basic PySpark DataFrames.
- Perform basic data transformations and aggregations using PySpark.
- Describe a basic end-to-end Big Data workflow.

</details>

<details><summary>Description</summary>

## Introduction

The previous modules introduced:

- What Big Data is
- The 6 V's of Big Data
- The components of a Big Data system
- The flow of data through a Big Data architecture

This module focuses on how these concepts can be implemented using common Big Data technologies.

The primary technologies covered are:

- Hadoop
- HDFS
- MapReduce
- Apache Spark
- PySpark

---

## What is Hadoop?

Hadoop is a distributed framework designed to store and process large datasets across multiple machines.

Instead of depending on a single machine, Hadoop distributes data and processing across a cluster.

A simplified Hadoop workflow is:

```text
Large Dataset
      ↓
Distributed Storage
      ↓
Distributed Processing
      ↓
Results
```

Hadoop is designed around concepts such as:

- Distributed storage
- Distributed processing
- Scalability
- Fault tolerance

---

## Hadoop Distributed File System (HDFS)

HDFS is a distributed file system used to store large files across multiple machines.

Instead of storing an entire large file on one machine, HDFS divides the file into blocks and distributes those blocks across nodes.

```text
Large File
     ↓
Split into Blocks
     ↓
┌────────┬────────┬────────┐
│Block 1 │Block 2 │Block 3 │
└────────┴────────┴────────┘
     ↓        ↓        ↓
   Node 1   Node 2   Node 3
```

HDFS is designed to provide:

- Distributed storage
- Scalability
- Fault tolerance
- Reliable access to large datasets

---

## HDFS Components

### NameNode

The NameNode manages metadata about files and directories in HDFS.

It keeps track of information such as:

- File names
- Directory structure
- File blocks
- Locations of blocks

The NameNode does not normally store the actual user data blocks.

### DataNode

DataNodes store the actual data blocks.

DataNodes communicate with the NameNode and perform operations involving the stored data.

Simplified architecture:

```text
             NameNode
          Metadata Manager
                │
       ┌────────┼────────┐
       ↓        ↓        ↓
   DataNode  DataNode  DataNode
   Blocks    Blocks    Blocks
```

---

## HDFS Blocks and Replication

HDFS divides large files into blocks.

Blocks can be replicated across multiple DataNodes.

Replication helps provide fault tolerance.

For example:

```text
Block A
  ├── DataNode 1
  ├── DataNode 2
  └── DataNode 3
```

If one DataNode becomes unavailable, another replica can be used.

This helps prevent data loss caused by individual node failures.

---

## Hadoop MapReduce

MapReduce is a distributed batch-processing model.

It processes large datasets by dividing the work across multiple machines.

The basic model consists of:

```text
Input
  ↓
Map
  ↓
Reduce
  ↓
Output
```

### Map Phase

The Map phase processes input data and produces intermediate key-value pairs.

For example, a word-count operation may transform input into:

```text
("hello", 1)
("big", 1)
("data", 1)
("hello", 1)
```

### Reduce Phase

The Reduce phase combines intermediate results.

For example:

```text
("hello", 2)
("big", 1)
("data", 1)
```

MapReduce is useful for distributed batch processing of large datasets.

---

## Apache Spark

Apache Spark is a distributed data-processing framework.

Spark can support:

- Batch processing
- DataFrame processing
- SQL operations
- Streaming workloads
- Machine learning workloads

Spark can perform many operations efficiently and can use in-memory processing to reduce repeated disk access.

---

## Hadoop MapReduce vs Spark

| Feature | MapReduce | Spark |
|---|---|---|
| Processing | Primarily batch | Batch and other workloads |
| Intermediate data | Commonly written to disk | Can use memory for intermediate processing |
| Processing speed | Generally slower for iterative workloads | Generally faster for many iterative workloads |
| APIs | Map and Reduce model | DataFrames, SQL, APIs |
| Python support | More limited | PySpark |

The choice of technology depends on the requirements of the workload.

---

## What is PySpark?

PySpark is the Python API for Apache Spark.

It allows developers to use Python to work with Spark's distributed processing capabilities.

PySpark is commonly used for:

- Data processing
- Data transformation
- Data analysis
- Data aggregation
- Data engineering
- Machine learning workflows

---

## PySpark DataFrames

A DataFrame is a distributed collection of data organized into named columns.

For example:

```text
+----------+----------+------+
| product  | quantity | price|
+----------+----------+------+
| Laptop   | 2        | 800  |
| Phone    | 5        | 500  |
| Tablet   | 3        | 300  |
+----------+----------+------+
```

PySpark provides operations for:

- Selecting columns
- Filtering rows
- Grouping data
- Aggregating values
- Sorting
- Transforming data

---

## Basic PySpark Workflow

A typical PySpark workflow is:

```text
Read Data
    ↓
Create DataFrame
    ↓
Inspect Data
    ↓
Transform Data
    ↓
Aggregate Data
    ↓
Analyze Results
    ↓
Write Output
```

</details>

<details><summary>Real World Application</summary>

## E-Commerce Sales Analysis

An e-commerce company stores millions of transaction records.

Each transaction may contain:

- Customer information
- Product information
- Quantity
- Price
- Transaction timestamp

A Big Data workflow can be used to calculate:

- Total sales
- Sales by product
- Most purchased products
- Customer purchase trends

A simplified architecture is:

```text
E-Commerce Transactions
          ↓
        HDFS
          ↓
       PySpark
          ↓
     DataFrame
          ↓
 Transform / Aggregate
          ↓
       Results
```

This demonstrates how distributed storage and processing technologies can work together to analyze large datasets.

</details>

<details><summary>Implementation</summary>

## End-to-End Big Data Workflow Using Hadoop and PySpark

Consider a dataset containing e-commerce sales.

### Step 1: Collect Data

Data may come from:

- Applications
- Transaction systems
- CSV files
- JSON files
- Application logs

Example:

```text
sales.csv
```

---

### Step 2: Store Data in HDFS

The sales data can be stored in HDFS.

Conceptually:

```text
sales.csv
    ↓
HDFS
    ↓
Distributed Blocks
    ↓
Multiple DataNodes
```

HDFS provides distributed storage and fault tolerance.

---

### Step 3: Read the Data Using PySpark

PySpark can read the data and create a DataFrame.

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
        .appName("SalesAnalysis")
        .getOrCreate()
)

df = spark.read.csv(
    "hdfs://path/to/sales.csv",
    header=True,
    inferSchema=True
)

df.show()
```

---

### Step 4: Transform the Data

PySpark can be used to filter, select, and transform records.

For example:

```python
result = df.filter(df.amount > 100)
```

This selects transactions where the amount is greater than 100.

---

### Step 5: Aggregate the Data

Data can be grouped and aggregated.

For example:

```python
result = df.groupBy("product_name").sum("amount")
```

This calculates the total sales amount for each product.

---

### Step 6: Display the Results

```python
result.show()
```

The results can then be used for further analysis or reporting.

---

## Complete Example

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
        .appName("SalesAnalysis")
        .getOrCreate()
)

df = spark.read.csv(
    "hdfs://path/to/sales.csv",
    header=True,
    inferSchema=True
)

result = df.groupBy("product_name").sum("amount")

result.show()

spark.stop()
```

---

## Key Implementation Concepts

### Distributed Storage

HDFS distributes data across multiple machines.

### Distributed Processing

Spark can distribute processing workloads across multiple machines.

### Parallel Execution

Multiple tasks can execute simultaneously across the cluster.

### Fault Tolerance

Distributed systems can continue operating when individual nodes fail, depending on the architecture and configuration.

### Scalability

Additional machines can be added to increase the capacity of the system.

---

## End-to-End Architecture

The concepts covered in this module can be combined into the following workflow:

```text
                DATA SOURCES
                     ↓
               DATA INGESTION
                     ↓
                   HDFS
                     ↓
              Hadoop / Spark
                     ↓
                  PySpark
                     ↓
                DataFrame
                     ↓
          Transform / Aggregate
                     ↓
                Data Analysis
                     ↓
             Reporting / Output
```

This workflow connects the concepts introduced throughout the Big Data curriculum.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Hadoop provides a framework for distributed Big Data storage and processing.
- HDFS provides distributed storage for large datasets.
- The NameNode manages HDFS metadata.
- DataNodes store actual data blocks.
- HDFS replication provides fault tolerance.
- MapReduce provides a distributed batch-processing model.
- Apache Spark provides distributed data-processing capabilities.
- PySpark allows developers to use Python with Apache Spark.
- PySpark DataFrames provide a convenient way to process structured data.
- Big Data workflows can combine HDFS and PySpark to store, process, and analyze large datasets.

The overall workflow is:

```text
Collect
  ↓
Store
  ↓
Process
  ↓
Analyze
  ↓
Report
```

These concepts provide a foundation for further learning in Big Data engineering and analytics.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
