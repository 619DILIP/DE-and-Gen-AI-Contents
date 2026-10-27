<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Identify the major technologies and components commonly used in Big Data environments.
- Explain the purpose of distributed storage.
- Explain the role of Hadoop and HDFS in Big Data systems.
- Describe the basic purpose of Hadoop MapReduce.
- Explain the role of Apache Spark in distributed data processing.
- Explain what PySpark is and how it is used.
- Differentiate between storage and processing components.
- Recognize how different technologies contribute to a Big Data ecosystem.

</details>

<details><summary>Description</summary>

## Introduction to Big Data Components

A Big Data environment uses multiple technologies to store, process, and analyze large and complex datasets.

Each technology or component has a specific role.

At a high level:

```text
Big Data Ecosystem
│
├── Distributed Storage
│   └── HDFS
│
├── Distributed Processing
│   ├── Hadoop MapReduce
│   └── Apache Spark
│
├── Data Analysis
│   └── Spark / PySpark
│
└── Supporting Components
    └── Additional tools and platforms
```

The purpose of this module is to introduce the major components and explain what each one does.

---

## Hadoop

Hadoop is a distributed framework designed to store and process large datasets across multiple machines.

Instead of depending on a single computer, Hadoop can distribute data and processing across a cluster.

Hadoop is associated with key concepts such as:

- Distributed storage
- Distributed processing
- Scalability
- Fault tolerance

---

## Hadoop Distributed File System (HDFS)

HDFS is a distributed file system designed to store large files across multiple machines.

Instead of storing an entire large file on one machine, HDFS divides files into blocks and distributes those blocks across DataNodes.

Conceptually:

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

HDFS provides:

- Distributed storage
- Scalability
- Fault tolerance
- Reliable storage of large datasets

Detailed HDFS implementation, including NameNode, DataNode, blocks, and replication, is covered in the **Big Data Fresher** module.

---

## Hadoop MapReduce

MapReduce is Hadoop's distributed batch-processing model.

It allows large datasets to be processed by dividing the work across multiple machines.

The basic processing model is:

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

For example, a word-count operation could produce:

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

MapReduce is primarily associated with distributed batch processing.

A practical MapReduce example is covered in the **Big Data Fresher** module.

---

## Apache Spark

Apache Spark is a distributed data-processing framework.

Spark can support:

- Batch processing
- DataFrame processing
- SQL operations
- Streaming workloads
- Machine learning workloads

Spark is designed to perform distributed processing efficiently and can use in-memory processing to reduce repeated disk access.

Spark can process data across multiple machines rather than relying entirely on a single computer.

---

## PySpark

PySpark is the Python API for Apache Spark.

It allows developers to use Python to work with Spark's distributed processing capabilities.

PySpark is commonly used for:

- Data processing
- Data transformation
- Data analysis
- Data aggregation
- Data engineering
- Machine learning workflows

The practical use of PySpark is covered in the **Big Data Fresher** module.

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

DataFrames make it possible to perform common data operations such as:

- Selecting columns
- Filtering rows
- Grouping data
- Aggregating values
- Sorting data
- Transforming data

---

## Storage Components vs Processing Components

One of the most important distinctions in a Big Data environment is between **storage** and **processing**.

### Storage

Storage components are responsible for keeping data.

Example:

- HDFS

```text
Data
 ↓
HDFS
 ↓
Distributed Storage
```

### Processing

Processing components are responsible for performing operations on stored data.

Examples:

- Hadoop MapReduce
- Apache Spark

```text
Stored Data
     ↓
Processing Framework
     ↓
Processed Results
```

Storage and processing work together, but they have different responsibilities.

---

## Hadoop and Spark

Hadoop and Spark are both important technologies in the Big Data ecosystem, but they are not identical.

Hadoop is commonly associated with:

- HDFS for distributed storage
- MapReduce for distributed batch processing

Spark is a distributed processing framework that supports:

- Batch processing
- DataFrames
- SQL
- Streaming
- Machine learning

A Big Data environment can use Hadoop storage together with Spark processing.

For example:

```text
HDFS
  ↓
Apache Spark
  ↓
PySpark
  ↓
Data Analysis
```

The specific technologies used depend on the requirements of the system.

---

## Big Data Components at a Glance

| Component / Technology | Primary Role |
|---|---|
| Hadoop | Distributed Big Data framework |
| HDFS | Distributed storage |
| NameNode | HDFS metadata management |
| DataNode | HDFS data storage |
| MapReduce | Distributed batch processing |
| Apache Spark | Distributed data processing |
| PySpark | Python API for Spark |
| DataFrame | Structured data representation for processing |

The detailed responsibilities of NameNode and DataNode, as well as practical use of HDFS and PySpark, are covered in the **Big Data Fresher** module.

---

## Relationship to Big Data Architecture

The technologies introduced in this module become components within a larger Big Data architecture.

For example:

```text
Data Sources
      ↓
Data Ingestion
      ↓
HDFS
      ↓
MapReduce / Spark
      ↓
Data Analysis
      ↓
Reporting
```

This diagram provides only a high-level view of how the technologies may be used.

</details>

<details><summary>Real World Application</summary>

## E-Commerce Data Processing

An e-commerce company can generate large amounts of data from:

- Customer transactions
- Product information
- Website activity
- Application logs
- Inventory systems

A Big Data environment may use distributed storage and processing technologies to work with this information.

For example:

```text
Customer / Application Data
          ↓
       HDFS
          ↓
    Spark / PySpark
          ↓
   Data Processing
          ↓
    Business Analysis
```

HDFS can provide distributed storage, while Spark or PySpark can process the stored data.

</details>

<details><summary>Implementation</summary>

## High-Level Component Selection

When designing a Big Data solution, different components are selected according to the requirements.

### Storage Requirement

If the system needs distributed storage for large datasets, a technology such as HDFS can be used.

### Batch Processing Requirement

If large datasets need to be processed as batches, Hadoop MapReduce can be used.

### Fast Distributed Processing Requirement

If the system requires distributed processing for analytics and other workloads, Apache Spark can be used.

### Python-Based Processing Requirement

If developers prefer Python for Spark-based processing, PySpark can be used.

---

## Example Component Selection

Consider an organization that needs to process large amounts of sales data.

A simplified technology selection could be:

```text
Large Sales Dataset
        ↓
      HDFS
        ↓
  Apache Spark
        ↓
     PySpark
        ↓
     Analysis
```

The purpose of this module is to understand the role of each component.

</details>

<details><summary>Summary</summary>

In this module, we explored the major components of the Big Data ecosystem:

- Hadoop provides a distributed framework for large-scale data storage and processing.
- HDFS provides distributed storage.
- MapReduce provides distributed batch processing.
- Apache Spark provides distributed data processing.
- PySpark provides a Python interface for Apache Spark.
- DataFrames provide a structured way to work with data in Spark.
- Storage and processing are separate responsibilities that can work together in a Big Data environment.

The key distinction is:

```text
HDFS       → Storage
MapReduce  → Batch Processing
Spark      → Distributed Processing
PySpark    → Python API for Spark
```

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
