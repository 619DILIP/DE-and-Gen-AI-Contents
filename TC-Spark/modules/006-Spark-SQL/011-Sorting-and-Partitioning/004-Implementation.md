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