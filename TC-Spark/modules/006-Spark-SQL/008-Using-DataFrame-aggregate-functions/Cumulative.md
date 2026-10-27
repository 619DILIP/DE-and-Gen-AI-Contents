<details><summary>Learning Objectives</summary>

After completing this module, learners should be able to:

- Understand aggregate functions in Spark DataFrames
- Apply built-in aggregation functions
- Perform grouped aggregations using groupBy()
- Use multiple aggregation functions together
- Interpret aggregated results correctly

</details>

<details><summary>Description</summary>

## Introduction to Aggregate Functions

Aggregate functions compute summary values from a collection of rows.

They are commonly used to:

- Count records
- Calculate averages
- Find minimum and maximum values
- Compute sums
- Determine distinct counts

When applied with groupBy(), they generate results per group.

---

## Common Aggregate Functions in Spark

---

Function Description

---

| Function                | Description                                            |
| ----------------------- | ------------------------------------------------------ |
| count()                 | Returns total number of rows                           |
| countDistinct()         | Returns number of distinct values                      |
| approx_count_distinct() | Approximate distinct count (faster for large datasets) |
| sum()                   | Returns sum of values                                  |
| avg()                   | Returns average value                                  |
| min()                   | Returns minimum value                                  |
| max()                   | Returns maximum value                                  |
| first()                 | Returns first value                                    |
| last()                  | Returns last value                                     |
| collect_list()          | Collects values including duplicates                   |
| collect_set()           | Collects unique values                                 |

---

## Grouped Aggregations

Using:

groupBy("column").agg()

Example use cases:

- Total sales per department
- Average salary per team
- Distinct product count per category

---

## When to Use approx_count_distinct()

For very large datasets where exact distinct counting is expensive.

It provides faster approximate results using probabilistic algorithms.

---

## Combining Multiple Aggregations

Multiple aggregate functions can be used together in agg():

df.groupBy("department").agg(sum("salary"), avg("salary"))

---

## Null Handling

Most aggregate functions ignore null values by default.

Functions like first() and last() support ignoreNulls parameter.

</details>

<details><summary>Real World Application</summary>

## 1. Sales Analytics

Compute total revenue per region using sum().

---

## 2. HR Analytics

Calculate average salary per department using avg().

---

## 3. Customer Insights

Find distinct customers using countDistinct().

---

## 4. Fraud Detection

Detect anomalies by analyzing minimum and maximum transaction values.

---

## 5. Product Analytics

Collect product categories per user using collect_set().

</details>

<details><summary>Implementation</summary>

## Step 1: Create SparkSession

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import *

spark = (
    SparkSession.builder
    .appName("AggregateFunctionsExample")
    .getOrCreate()
)
```

---

## Step 2: Create Sample DataFrame

```python
data = [
    ("James", "Sales", 3000),
    ("Michael", "Sales", 4600),
    ("Robert", "Sales", 4100),
    ("Maria", "Finance", 3000),
    ("Scott", "Finance", 3300),
    ("Jen", "Finance", 3900),
    ("Jeff", "Marketing", 3000),
    ("Kumar", "Marketing", 2000),
    ("Saif", "Sales", 4100)
]

columns = ["employee_name", "department", "salary"]

df = spark.createDataFrame(data, columns)
df.show()
```

---

## Step 3: Basic Aggregations

### Count

```python
df.select(count("salary")).show()
```

### Distinct Count

```python
df.select(countDistinct("department")).show()
```

### Approximate Distinct

```python
df.select(approx_count_distinct("salary")).show()
```

### Average

```python
df.select(avg("salary")).show()
```

### Minimum & Maximum

```python
df.select(min("salary"), max("salary")).show()
```

### Sum

```python
df.select(sum("salary")).show()
```

---

## Step 4: collect_list and collect_set

```python
df.select(collect_list("salary")).show(truncate=False)
df.select(collect_set("salary")).show(truncate=False)
```

---

## Step 5: Grouped Aggregation

```python
df.groupBy("department").agg(
    sum("salary").alias("total_salary"),
    avg("salary").alias("average_salary"),
    count("employee_name").alias("employee_count")
).show()
```

---

## Step 6: First and Last

```python
df.select(first("salary"), last("salary")).show()
```

---

## Step 7: Explain Execution Plan

```python
df.groupBy("department").sum("salary").explain(True)
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Aggregate functions summarize data
- count(), sum(), avg(), min(), and max() are commonly used
- countDistinct() finds unique values
- approx_count_distinct() improves performance for large datasets
- collect_list() and collect_set() gather grouped values
- groupBy() enables grouped aggregations
- Aggregations are optimized internally by Spark SQL

Aggregate functions are essential for analytics, reporting, and data
summarization in Spark applications.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
