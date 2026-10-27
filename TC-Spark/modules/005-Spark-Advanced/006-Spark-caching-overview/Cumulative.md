<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define Spark caching and persistence
- Understand how Spark cache works internally
- Identify when caching should be used
- Differentiate between cache() and persist()
- Understand storage levels in Spark
- Apply caching in RDDs and DataFrames
- Improve Spark application performance using caching

</details>

<details><summary>Description</summary>

## What is Spark Caching?

Spark Caching is a mechanism used to store intermediate computation
results in memory (or disk) so that they can be reused without
recomputation.

When we call:

- cache()
- persist()

on an RDD or DataFrame, Spark marks that dataset for storage after the
first action is triggered.

Important:

- Caching is lazy.
- Data is cached only after the first action executes.
- It improves performance when the same dataset is reused multiple
  times.

---

## Why Spark Caching is Important

Spark follows a lazy evaluation model. Every time an action is
triggered, Spark recomputes the entire lineage unless the intermediate
result is cached.

Without caching:

Data → Transformations → Action\
(recomputed every time)

With caching:

Data → Transformations → Cached Result → Multiple Actions\
(no recomputation)

---

## When to Use Spark Cache

Use caching when:

- A DataFrame or RDD is reused multiple times
- Multiple actions are applied on the same dataset
- Iterative algorithms (e.g., Machine Learning)
- Complex transformations that are expensive
- ETL pipelines where intermediate results are reused

Avoid caching when:

- Dataset is used only once
- Dataset is too large for available memory
- Recomputing is cheaper than storing

---

## cache() vs persist()

### cache()

Equivalent to:

persist(StorageLevel.MEMORY_ONLY)

Stores data in memory only.

---

### persist()

Allows specifying storage level:

Examples:

- MEMORY_ONLY
- MEMORY_AND_DISK
- DISK_ONLY
- MEMORY_ONLY_SER
- MEMORY_AND_DISK_SER

Example:

```python
from pyspark import StorageLevel
df.persist(StorageLevel.MEMORY_AND_DISK)
```

---

## How Spark Cache Works Internally

1.  cache() marks dataset as cacheable.
2.  First action triggers execution.
3.  Spark stores partitions in executor memory.
4.  Subsequent actions reuse cached partitions.
5.  Cache Manager tracks cached datasets.

Cached data resides in executor memory, not driver memory.

</details>

<details><summary>Real World Application</summary>

## 1. Machine Learning Pipelines

Training algorithms iterate multiple times over the same dataset.
Caching prevents recomputation of feature transformations.

---

## 2. Interactive Analytics

Data scientists run multiple queries on the same dataset. Caching
improves query response time.

---

## 3. ETL Pipelines

Intermediate cleansed data reused for: - Aggregations - Joins -
Reporting

Caching improves throughput.

---

## 4. Streaming Applications

Repeated micro-batch computations can reuse cached intermediate data.

---

</details>

<details><summary> Implementation </summary>

## Example 1: Caching RDD

```python
rdd = spark.sparkContext.textFile("data.txt")

processed = rdd.map(lambda x: x.split(","))

processed.cache()

processed.count()   # First action triggers caching
processed.collect() # Uses cached data
```

---

## Example 2: Caching DataFrame

```python
df = spark.read.csv("data.csv", header=True, inferSchema=True)

filtered_df = df.filter(df["age"] > 25)

filtered_df.cache()

filtered_df.count()
filtered_df.show()
```

---

## Example 3: Using persist()

```python
from pyspark import StorageLevel

df.persist(StorageLevel.MEMORY_AND_DISK)

df.count()
```

---

## Example 4: Unpersisting Data

To remove cached data:

```python
df.unpersist()
```

---

## Spark SQL Caching

```python
spark.sql("CACHE TABLE table_name")
spark.sql("CACHE LAZY TABLE table_name")
spark.sql("UNCACHE TABLE table_name")
```

---

## Checking Cached Data in Spark UI

1.  Open Spark UI
2.  Navigate to Storage tab
3.  Observe cached RDD/DataFrame details

</details>

<details><summary> Summary </summary>

In this module, we learned:

- Spark caching stores intermediate results in memory or disk
- cache() uses MEMORY_ONLY storage by default
- persist() allows flexible storage levels
- Caching is useful for repeated actions and iterative processing
- Data is cached only after first action
- unpersist() removes cached data
- Proper caching improves performance significantly

Spark caching is a powerful optimization technique for distributed data
processing systems.

</details>

<details><summary> Practice Questions </summary>

[Practice Questions](./Quiz.gift)

</details>
