<details><summary>Learning Objectives</summary>

After completing this module, learners should be able to:

- Differentiate between Hadoop, MapReduce, and Apache Spark.
- Compare performance characteristics of MapReduce and Spark.
- Explain architectural differences.
- Identify suitable use cases for each framework.
- Understand trade-offs in cost, latency, and scalability.

</details>

<details><summary>Description</summary>

## Understanding the Components

Before comparing, it is important to clarify the roles:

- **Hadoop** is an ecosystem for distributed storage and processing.
- **MapReduce** is Hadoop’s original processing model.
- **Spark** is a separate distributed data processing engine that can run independently or on Hadoop (via YARN).

Hadoop includes:
- HDFS (Storage)
- YARN (Resource Management)
- MapReduce (Processing)

Spark can:
- Run on YARN
- Use HDFS for storage
- Replace MapReduce as a processing engine

# Key Differences

## 1. Speed

### Apache Spark
- Processes data in memory.
- Up to 100× faster in-memory.
- Around 10× faster on disk compared to MapReduce.
- Reduces disk read/write cycles.

### Hadoop MapReduce
- Disk-based processing.
- Writes intermediate data to disk.
- Slower due to repeated disk I/O.

---

## 2. Ease of Use

### Apache Spark
- Provides high-level APIs.
- Supports Scala, Python, Java, and R.
- Uses RDDs and DataFrames.
- Supports interactive processing.

### Hadoop MapReduce
- Requires writing Map and Reduce logic manually.
- More boilerplate code.
- No interactive mode.
- More complex development.

---

## 3. Latency

### Apache Spark
- Low latency.
- Suitable for real-time and interactive analytics.

### Hadoop MapReduce
- High latency.
- Designed primarily for batch processing.

---

## 4. Data Processing Capabilities

### Apache Spark
Supports:
- Batch processing
- Streaming
- Machine learning
- Graph processing
- Interactive SQL

### Hadoop MapReduce
Supports:
- Batch processing only

---

## 5. Failure Recovery

### Hadoop MapReduce
- Strong fault tolerance.
- Resumes failed tasks automatically.
- Based on disk-based checkpoints.

### Apache Spark
- Fault tolerance via lineage (RDD).
- Recomputes lost partitions.
- Efficient but memory-heavy workloads may require tuning.

---

## 6. Cost Consideration

### Hadoop MapReduce
- Requires less memory.
- Lower hardware cost.
- Suitable for budget-constrained batch workloads.

### Apache Spark
- Memory-intensive.
- Requires higher RAM.
- Higher infrastructure cost.

---

## 7. Security

Both integrate with Hadoop ecosystem security:

- Kerberos authentication
- HDFS permissions
- YARN-based access control

Security depends on configuration rather than framework default.

---

# Comparison Table

| Factor | MapReduce | Spark |
|---------|------------|--------|
| Processing Type | Batch | Batch + Streaming + ML |
| Speed | Disk-based, slower | In-memory, much faster |
| Ease of Use | Complex | High-level APIs |
| Latency | High | Low |
| Interactive Mode | No | Yes |
| Machine Learning | Limited | Built-in MLlib |
| Graph Processing | No native support | GraphX |
| Streaming | Not supported | Spark Streaming |
| Memory Usage | Low | High |
| Suitable For | Large batch jobs | Real-time & advanced analytics |

</details>

<details><summary>Real World Application</summary>

## Hadoop MapReduce Use Case

Imagine you have 10 large datasets (bags of data).  
Each mapper processes one dataset in parallel.  
The reducer aggregates the results.

Used for:
- Daily ETL jobs
- Log aggregation
- Data warehousing batch tasks

Industries:
- Banking
- Telecom
- Government archives

---

## Apache Spark Use Case

Spark is used when real-time speed matters.

Example:
- Real-time fraud detection
- Recommendation systems
- Live dashboard analytics
- Streaming analytics

Industries:
- E-commerce
- FinTech
- Media platforms
- Machine learning pipelines

---

## When to Choose What?

Choose MapReduce when:
- Processing large historical batch datasets
- Budget constraints exist
- Simpler batch pipeline required

Choose Spark when:
- Low latency is required
- Machine learning needed
- Interactive analytics required
- Real-time streaming required

</details>

<details><summary>Implementation</summary>

## 1️⃣ Hadoop MapReduce (Python via Hadoop Streaming)

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

### Execution

``` bash
hadoop jar hadoop-streaming.jar \
-input input.txt \
-output output \
-mapper mapper.py \
-reducer reducer.py
```

------------------------------------------------------------------------

## 2️⃣ Apache Spark (PySpark)

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("WordCount").getOrCreate()

text_file = spark.read.text("input.txt")

words = text_file.rdd.flatMap(lambda line: line.value.split())

word_counts = words.map(lambda word: (word, 1)).reduceByKey(lambda a, b: a + b)

word_counts.saveAsTextFile("output")

spark.stop()
```

### Execution

``` bash
spark-submit wordcount.py
```

------------------------------------------------------------------------

## Key Implementation Differences

| Aspect                | MapReduce                     | Spark            |
|------------------------|--------------------------------|------------------|
| Code Structure         | Separate mapper & reducer      | Single script    |
| Intermediate Data      | Written to disk                | Stored in memory |
| Development Speed      | Slower                         | Faster           |
| Iterative Processing   | Inefficient                    | Efficient        |


</details>

<details><summary>Summary</summary>
In this module, we learned:

- Hadoop is an ecosystem.
- MapReduce is a batch processing model within Hadoop.
- Spark is a fast, in-memory processing engine.
- Spark outperforms MapReduce in speed and flexibility.
- MapReduce remains relevant for cost-effective batch workloads.
- Spark is preferred for real-time and advanced analytics.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
