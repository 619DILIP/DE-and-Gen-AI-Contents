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