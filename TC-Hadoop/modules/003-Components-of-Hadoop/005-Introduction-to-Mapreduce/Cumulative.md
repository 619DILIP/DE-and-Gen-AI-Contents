<details><summary>Learning Overview</summary>

After completing this module, associates should be able to:

-   Explain the purpose of MapReduce in big data processing.
-   Describe the complete lifecycle of a MapReduce job.
-   Understand how key-value pairs are transformed across phases.
-   Explain how fault tolerance and parallelism are achieved.
-   Identify enterprise-level use cases.
-   Implement and execute a basic MapReduce job using Hadoop Streaming.
-   Differentiate between single and multiple reducer configurations.

</details>

<details><summary>Description</summary>

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


</details>

<details><summary>Real World Application</summary>

## Enterprise Use Cases

### E-Commerce

-   Customer purchase analysis
-   Recommendation engines
-   Sales reporting

### Social Media

-   Engagement tracking
-   Trend analysis
-   Graph processing

### Entertainment Platforms

-   Viewing pattern analysis
-   Personalized recommendations

### Financial Institutions

-   Fraud detection
-   Risk modeling
-   Transaction aggregation

### Telecom Industry

-   Call record analysis
-   Network monitoring

</details>

<details><summary>Implementation</summary>

## Example: Word Count using Hadoop Streaming

### Mapper (mapper.py)

``` python
#!/usr/bin/env python
import sys

for line in sys.stdin:
    words = line.strip().split()
    for word in words:
        print(f"{word}\t1")
```

### Reducer (reducer.py)

``` python
#!/usr/bin/env python
import sys
from itertools import groupby
from operator import itemgetter

def read_mapper_output(file, separator='\t'):
    for line in file:
        yield line.rstrip().split(separator, 1)

data = read_mapper_output(sys.stdin)

for current_word, group in groupby(data, itemgetter(0)):
    try:
        total_count = sum(int(count) for _, count in group)
        print(f"{current_word}\t{total_count}")
    except ValueError:
        pass
```

### Execution Command

``` bash
hadoop jar hadoop-streaming.jar \
-input input.txt \
-output output \
-mapper mapper.py \
-reducer reducer.py
```

### Execution Flow

1.  Input file stored in HDFS
2.  Hadoop splits the file
3.  Mapper processes each split
4.  Shuffle groups identical keys
5.  Reducer aggregates results
6.  Output stored in HDFS

</details>

<details><summary>Summary</summary>

In this module, we learned:

-   MapReduce is a distributed processing model.
-   It operates in Map, Shuffle/Sort, and Reduce phases.
-   Uses key-value pairs for data transformation.
-   Provides automatic parallelism and fault tolerance.
-   Scales across large clusters in enterprise environments.

</details>

