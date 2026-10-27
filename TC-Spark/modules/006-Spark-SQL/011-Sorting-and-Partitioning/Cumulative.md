<details><summary>Learning Objectives</summary>

After completing this module, learners should be able to:

- Understand the concept of partitioning in Spark
- Explain how Spark distributes data across partitions
- Apply repartition() and coalesce() effectively
- Perform sorting on DataFrames using different methods
- Understand the performance impact of sorting and partitioning
- Optimize partitioning strategies in Spark applications

</details>

<details><summary>Description</summary>

## Introduction to Partitioning

Partitioning in Spark refers to dividing a dataset into smaller logical
chunks called partitions.

Each partition:

- Is processed in parallel
- Resides on a single executor
- Corresponds to one task during execution

Proper partitioning improves:

- Parallelism
- Resource utilization
- Performance

---

## Default Partitioning Behavior

### Local Mode

When running in local mode:

The number of partitions typically equals the number of cores specified
in:

spark = SparkSession.builder.master("local\[5\]").getOrCreate()

This creates 5 parallel partitions.

---

### Cluster Mode

In distributed clusters:

Partitions are influenced by:

- HDFS block size
- Total executor cores
- spark.sql.shuffle.partitions (default 200)

For example:

If HDFS block size is 128 MB and file size is 640 MB:

640 / 128 = 5 partitions

---

## Repartition vs Coalesce

### repartition()

- Increases or decreases partitions
- Causes full shuffle
- Expensive operation

### coalesce()

- Reduces partitions
- Avoids full shuffle (when decreasing)
- More efficient for reducing partitions

---

## Partitioning While Writing Data

Use partitionBy():

df.write.partitionBy("column_name").parquet("output_path")

This creates folder-based partitioning on disk.

---

## Introduction to Sorting

Sorting arranges data in ascending or descending order.

Spark provides:

- sort()
- orderBy()
- asc()
- desc()
- asc_nulls_first()
- desc_nulls_last()

Sorting triggers shuffle when applied globally.

---

## Global vs Local Sorting

- orderBy() → Global sort (shuffle required)
- sortWithinPartitions() → Sort inside each partition only

---

## Performance Considerations

- Sorting large datasets can be expensive
- Repartitioning unnecessarily increases shuffle
- Proper partition size improves efficiency
- Default shuffle partitions = 200

</details>

<details><summary>Real World Application</summary>

## 1. Data Lake Optimization

Partitioning large datasets by date improves query performance.

---

## 2. Log Processing

Sorting logs by timestamp helps chronological analysis.

---

## 3. Financial Transactions

Partitioning by region enables parallel processing.

---

## 4. Data Warehousing

Partition pruning improves query speed.

---

## 5. Report Generation

Sorted output ensures readable reports.

</details>

<details><summary>Implementation</summary>

## Step 1: Create SparkSession

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col

spark = (
    SparkSession.builder
    .appName("SortingPartitioningExample")
    .master("local[5]")
    .getOrCreate()
)
```

---

## Step 2: Check Default Partitions

```python
df = spark.range(0, 20)
print(df.rdd.getNumPartitions())
```

---

## Step 3: Repartition Data

```python
df_repartitioned = df.repartition(10)
print(df_repartitioned.rdd.getNumPartitions())
```

---

## Step 4: Coalesce Partitions

```python
df_coalesced = df_repartitioned.coalesce(4)
print(df_coalesced.rdd.getNumPartitions())
```

---

## Step 5: Create Sample DataFrame

```python
data = [
    ("Robert", "Sales", "CA", 81000, 31),
    ("Maria", "Finance", "CA", 90000, 21),
    ("Jeff", "Marketing", "CA", 80000, 23),
    ("Kumar", "Marketing", "NY", 91000, 34)
]

columns = ["E_name", "dept", "state", "salary", "age"]

df = spark.createDataFrame(data, columns)
df.show()
```

---

## Step 6: Sorting Examples

### Ascending Sort

```python
df.orderBy("dept", "state").show()
```

### Descending Sort

```python
df.orderBy(col("salary").desc()).show()
```

### Mixed Sorting

```python
df.orderBy(col("dept").asc(), col("salary").desc()).show()
```

---

## Step 7: Sort Within Partitions

```python
df.sortWithinPartitions("salary").show()
```

---

## Step 8: Partition While Writing

```python
df.write.partitionBy("dept").mode("overwrite").parquet("partition_output")
```

---

## Step 9: Check Shuffle Partitions

```python
print(spark.conf.get("spark.sql.shuffle.partitions"))
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Partitioning divides data for parallel processing
- Default partitions depend on execution environment
- repartition() triggers shuffle
- coalesce() reduces partitions efficiently
- Sorting can be global or partition-level
- Global sorting causes shuffle
- partitionBy() improves query performance in storage systems
- Proper partition strategy improves performance and reduces cost

Sorting and partitioning are essential techniques for scalable Spark
applications.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
