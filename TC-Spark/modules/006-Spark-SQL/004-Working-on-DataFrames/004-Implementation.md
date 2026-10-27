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