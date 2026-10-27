<details><summary>Learning Objectives</summary>

After completing this module, learners should be able to:

- Understand what Parquet format is
- Explain advantages of columnar storage
- Read Parquet files into Spark DataFrames
- Write DataFrames to Parquet format
- Use Parquet files with Spark SQL
- Understand partitioned Parquet storage
- Explain why Parquet improves performance

</details>

<details><summary>Description</summary>

## Introduction to Parquet

Parquet is a columnar storage file format widely used in big data
systems.

Unlike row-based formats (CSV, JSON), Parquet stores data column-wise.

---

## Why Parquet is Important

### 1. Columnar Storage

- Reads only required columns
- Reduces disk I/O
- Improves query performance

---

### 2. Compression & Encoding

- Uses efficient compression
- Type-specific encoding
- Reduces storage space

---

### 3. Schema Storage

- Stores schema along with data
- No need to redefine schema while reading

---

### 4. Predicate Pushdown

Spark can filter data at storage level, improving performance.

---

## Reading and Writing Parquet in Spark

Spark provides built-in support for:

- spark.read.parquet()
- df.write.parquet()

Schema is automatically preserved.

---

## Partitioned Parquet

While writing:

df.write.partitionBy("column").parquet("path")

This creates folder-based partitions on disk.

Example directory structure:

path/ department=Sales/ department=Finance/

Partition pruning improves performance.

---

## Advantages Over JSON/CSV

- Faster reads
- Lower storage size
- Better compression
- Optimized analytics workloads

</details>

<details><summary>Real World Application</summary>

## 1. Data Lakes

Organizations store large datasets in Parquet for efficient analytics.

---

## 2. ETL Pipelines

Intermediate processed data is stored in Parquet for faster downstream
queries.

---

## 3. Data Warehousing

Modern warehouses use Parquet as primary storage format.

---

## 4. Cloud Analytics

Parquet is widely used in AWS, Azure, and GCP storage systems.

---

## 5. Machine Learning

Training datasets are stored in Parquet for faster loading.

</details>

<details><summary>Implementation</summary>

## Step 1: Create SparkSession

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("ParquetExample")
    .getOrCreate()
)
```

---

## Step 2: Create Sample DataFrame

```python
data = [
    ("James", "Sales", 3000),
    ("Maria", "Finance", 4000),
    ("Robert", "Sales", 3500),
    ("Scott", "Finance", 4200)
]

columns = ["name", "department", "salary"]

df = spark.createDataFrame(data, columns)
df.show()
```

---

## Step 3: Write DataFrame to Parquet

```python
df.write.mode("overwrite").parquet("output/parquet_data")
```

---

## Step 4: Read Parquet File

```python
parquet_df = spark.read.parquet("output/parquet_data")
parquet_df.show()
```

---

## Step 5: Check Schema

```python
parquet_df.printSchema()
```

---

## Step 6: Partitioned Write

```python
df.write   .mode("overwrite")   .partitionBy("department")   .parquet("output/partitioned_parquet")
```

---

## Step 7: Query Using Spark SQL

```python
parquet_df.createOrReplaceTempView("employees")

spark.sql("SELECT department, AVG(salary) FROM employees GROUP BY department").show()
```

---

## Step 8: Explain Execution Plan

```python
parquet_df.filter(parquet_df.salary > 3500).explain(True)
```

Observe predicate pushdown in physical plan.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Parquet is a columnar storage format
- It improves performance by reading only required columns
- Spark automatically preserves schema in Parquet
- Partitioned Parquet improves query efficiency
- Parquet reduces storage and improves compression
- It is widely used in data lakes and analytics systems

Parquet is the preferred storage format for large-scale Spark analytics
workloads.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
