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