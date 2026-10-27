<details><summary>Learning Objectives</summary>

After completing this module, learners should be able to:

- Understand how DataFrames work internally
- Create DataFrames from multiple data sources
- Perform transformations and actions on DataFrames
- Manipulate columns and rows efficiently
- Apply filtering, aggregation, and joins
- Save DataFrames to storage systems

</details>

<details><summary>Description</summary>

## Introduction

A DataFrame is a distributed collection of data organized into named
columns.

It is conceptually similar to:

- A table in a relational database
- A spreadsheet
- A Pandas DataFrame (but distributed)

DataFrames are built on top of RDDs but provide:

- Schema awareness
- Catalyst query optimization
- Improved performance
- Declarative query capabilities

---

## Why DataFrames Are Important

DataFrames:

- Provide structured data processing
- Enable SQL-like operations
- Automatically optimize execution plans
- Improve readability and maintainability of code
- Support multiple data formats

They are the primary abstraction used in modern Spark applications.

---

## Key Characteristics of DataFrames

- Distributed across cluster nodes
- Immutable
- Schema-based
- Lazy evaluation
- Optimized by Catalyst
- Supports SQL queries

---

## Common Operations in DataFrames

### Column Operations

- select()
- withColumn()
- drop()
- rename()

### Row Operations

- filter()
- where()
- limit()

### Aggregations

- groupBy()
- agg()
- count()
- sum()
- avg()

### Joins

- inner join
- left join
- right join
- full outer join

### Sorting

- orderBy()
- sort()

---

## Data Sources

DataFrames can be created from:

- CSV
- JSON
- Parquet
- ORC
- JDBC
- Hive tables
- Existing RDDs

</details>

<details><summary>Real World Application</summary>

## 1. ETL Pipelines

DataFrames are widely used to clean, transform, and load large datasets.

---

## 2. Data Warehousing

Organizations use DataFrames for structured analytics on distributed
systems.

---

## 3. Log Processing

JSON or CSV logs are converted into DataFrames for analysis.

---

## 4. Business Reporting

Aggregations and joins generate summarized reports.

---

## 5. Machine Learning

DataFrames are used as inputs for ML pipelines.

</details>

<details><summary>Implementation</summary>

## Step 1: Create SparkSession

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("WorkingWithDataFrames")
    .getOrCreate()
)
```

---

## Step 2: Create DataFrame from Python List

```python
data = [(1, "John", 85),
        (2, "Paul", 90),
        (3, "Kale", 78)]

columns = ["id", "name", "marks"]

df = spark.createDataFrame(data, columns)
df.show()
```

---

## Step 3: Select Specific Columns

```python
df.select("name", "marks").show()
```

---

## Step 4: Filter Rows

```python
df.filter(df.marks > 80).show()
```

---

## Step 5: Add a New Column

```python
from pyspark.sql.functions import col

df = df.withColumn("grade_bonus", col("marks") + 5)
df.show()
```

---

## Step 6: Rename Column

```python
df = df.withColumnRenamed("marks", "score")
df.show()
```

---

## Step 7: Group By and Aggregate

```python
df.groupBy("name").sum("score").show()
```

---

## Step 8: Sort Data

```python
df.orderBy("score", ascending=False).show()
```

---

## Step 9: Join Example

```python
dept_data = [(1, "CS"), (2, "IT"), (3, "ECE")]
dept_columns = ["id", "department"]

dept_df = spark.createDataFrame(dept_data, dept_columns)

joined_df = df.join(dept_df, on="id", how="inner")
joined_df.show()
```

---

## Step 10: Read Data from CSV

```python
df_csv = spark.read.csv("student.csv", header=True, inferSchema=True)
df_csv.show()
```

---

## Step 11: Save DataFrame to Parquet

```python
df.write.mode("overwrite").parquet("output_parquet")
```

---

## Step 12: View Schema

```python
df.printSchema()
```

---

## Step 13: View Execution Plan

```python
df.explain(True)
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- DataFrames are structured distributed datasets
- They support SQL-like operations
- They are optimized using Catalyst
- Common operations include select, filter, groupBy, join, and orderBy
- DataFrames can read from and write to multiple data sources
- Execution plans can be inspected using explain()

Working with DataFrames is fundamental to building scalable Spark
applications.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
