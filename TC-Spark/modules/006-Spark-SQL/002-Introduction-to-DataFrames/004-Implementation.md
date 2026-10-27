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