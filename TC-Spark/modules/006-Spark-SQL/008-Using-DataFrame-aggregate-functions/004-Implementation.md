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