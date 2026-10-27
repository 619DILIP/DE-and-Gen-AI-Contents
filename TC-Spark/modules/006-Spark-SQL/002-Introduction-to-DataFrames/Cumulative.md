<details><summary>Learning Objectives</summary>

After completing this module, learners should be able to:

- Define what a DataFrame is in Spark
- Understand how DataFrames differ from RDDs
- Create DataFrames from various data sources
- Perform common transformations and actions on DataFrames
- Understand schema and its importance
- Use DataFrame APIs efficiently in Spark applications

</details>

<details><summary>Description</summary>

## What is a DataFrame?

A DataFrame in Spark is a distributed collection of data organized into
named columns.

It is:

- Similar to a table in a relational database
- Similar to a DataFrame in Pandas
- Built on top of RDDs
- Optimized by the Catalyst Optimizer

Unlike RDDs, DataFrames are schema-aware, meaning they know the
structure of the data.

---

## Why Use DataFrames?

DataFrames provide:

- Better optimization through Catalyst
- Automatic query optimization
- Simplified syntax
- Integration with Spark SQL
- Improved performance compared to RDDs

---

## RDD vs DataFrame

| Feature        | RDD              | DataFrame                     |
|---------------|------------------|-------------------------------|
| Schema        | No               | Yes                           |
| Optimization  | Limited          | Catalyst Optimizer            |
| Ease of Use   | More verbose     | SQL-like operations           |
| Performance   | Slower           | Faster                        |
| API Style     | Functional       | Declarative + Functional      |

---

## Key Characteristics of DataFrames

1.  Distributed and immutable
2.  Schema-based structure
3.  Lazy evaluation
4.  Supports SQL queries
5.  Optimized execution plan

---

## Common DataFrame Operations

### Transformations

- select()
- filter()
- groupBy()
- join()
- orderBy()
- withColumn()

### Actions

- show()
- collect()
- count()
- first()

---

## Schema in DataFrames

Schema defines:

- Column names
- Data types
- Nullability

Schema helps Spark optimize queries and reduce runtime errors.

---

## Data Sources Supported

DataFrames can read data from:

- CSV
- JSON
- Parquet
- ORC
- JDBC
- Hive tables

</details>

<details><summary>Real World Application</summary>

## 1. Data Warehousing

DataFrames are used to perform large-scale SQL analytics on distributed
data.

---

## 2. ETL Pipelines

DataFrames simplify data cleaning and transformation workflows.

---

## 3. Business Intelligence

DataFrames integrate with BI tools via Spark SQL.

---

## 4. Log Processing

JSON logs can be loaded into DataFrames and analyzed efficiently.

---

## 5. Machine Learning Pipelines

DataFrames are used as input for Spark ML pipelines.

</details>

<details><summary>Implementation</summary>

## Step 1: Create SparkSession

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("DataFrameExample")
    .getOrCreate()
)
```

---

## Step 2: Create DataFrame from List

```python
data = [("Alice", 25), ("Bob", 30), ("Charlie", 35)]
columns = ["name", "age"]

df = spark.createDataFrame(data, columns)
df.show()
```

---

## Step 3: Select Columns

```python
df.select("name").show()
```

---

## Step 4: Filter Rows

```python
df.filter(df.age > 28).show()
```

---

## Step 5: Add New Column

```python
from pyspark.sql.functions import col

df.withColumn("age_plus_5", col("age") + 5).show()
```

---

## Step 6: Group By Operation

```python
df.groupBy("age").count().show()
```

---

## Step 7: Read from CSV

```python
df_csv = spark.read.csv("data.csv", header=True, inferSchema=True)
df_csv.show()
```

---

## Step 8: View Schema

```python
df.printSchema()
```

---

## Step 9: Explain Execution Plan

```python
df.explain(True)
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A DataFrame is a structured distributed dataset
- DataFrames are schema-aware and optimized
- They provide better performance than RDDs
- DataFrames support SQL queries
- Common operations include select, filter, groupBy, and join
- Spark optimizes DataFrames using Catalyst

DataFrames are the foundation of modern Spark development and are widely
used in production environments.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
