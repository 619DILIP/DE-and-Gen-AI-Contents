## What is MapReduce?

MapReduce is a distributed programming model designed for processing
large-scale datasets across clusters of machines. It allows computation
to move closer to where data is stored, reducing network overhead and
improving performance.

It works closely with HDFS (Hadoop Distributed File System).

## Why MapReduce Was Introduced

Traditional systems struggled with:

-   Massive unstructured datasets
-   Distributed storage challenges
-   Fault handling in large clusters
-   Coordinating parallel tasks

MapReduce abstracts complex distributed logic so developers only need to
define:

1.  A Map function\
2.  A Reduce function

The framework handles splitting, scheduling, monitoring, and failure
recovery.

## Core Concept: Key-Value Pairs

MapReduce operates entirely on key-value pairs.

Each stage: - Accepts key-value pairs as input - Produces key-value
pairs as output

## Phases of MapReduce

### 1. Map Phase

-   Input file stored in HDFS
-   Divided into input splits
-   Each split processed by a mapper
-   Emits intermediate key-value pairs

Example:

Input: Hello Hadoop\
Hello World

Mapper Output: Hello 1\
Hadoop 1\
Hello 1\
World 1

### 2. Shuffle and Sort Phase

-   Sorts keys
-   Groups identical keys
-   Transfers grouped data to reducers

Grouped Output:

Hello \[1,1\]\
Hadoop \[1\]\
World \[1\]

### 3. Reduce Phase

-   Receives grouped keys
-   Aggregates values
-   Stores final output in HDFS

Final Output:

Hello 2\
Hadoop 1\
World 1

## Parallelism and Fault Tolerance

-   Multiple mappers run in parallel.
-   Multiple reducers can run in parallel.
-   Failed tasks are automatically restarted.
-   HDFS replication ensures reliability.

## Single vs Multiple Reducers

Single Reducer:
- All intermediate data sent to one reducer
- Produces a single output file
- May become a bottleneck

Multiple Reducers:
- Keys partitioned across reducers
- Multiple output files generated
- Better scalability for large datasets

## Data Flow Examples

### Example 1: MapReduce with a Single Reduce Task

![MapReduce Single Reducer](Images/MapReduce.png)

Explanation:
- Multiple splits processed by mappers
- All intermediate data shuffled to one reducer
- One output file generated in HDFS

### Example 2: MapReduce with Multiple Reduce Tasks

![MapReduce Multiple Reducers](Images/MapReduce1.png)

Explanation:
- Splits processed in parallel
- Keys partitioned across reducers
- Multiple output files generated
- Improved performance and scalability

## Limitations of MapReduce

- Disk-based processing between stages
- Not suitable for real-time workloads
- Inefficient for iterative algorithms
- Higher latency compared to in-memory engines