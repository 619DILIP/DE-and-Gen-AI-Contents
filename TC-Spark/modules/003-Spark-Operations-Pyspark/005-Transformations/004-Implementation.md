## Step 1: Create RDD

```python
from pyspark import SparkContext

sc = SparkContext("local[*]", "RDDTransformationExample")

data = [1, 2, 3, 3, 4, 5, 2]
rdd1 = sc.parallelize(data)
```

---

## map()

```python
rdd1.map(lambda x: x * 2).collect()
```

---

## filter()

```python
rdd1.filter(lambda x: x < 3).collect()
```

---

## distinct()

```python
rdd1.distinct().collect()
```

---

## flatMap()

```python
rdd = sc.parallelize(["hello world", "spark rdd"])
rdd.flatMap(lambda x: x.split(" ")).collect()
```

---

## union()

```python
rdd1 = sc.parallelize([1, 2, 3])
rdd2 = sc.parallelize([4, 5, 6])
rdd1.union(rdd2).collect()
```

---

## intersection()

```python
rdd1 = sc.parallelize([1, 2, 3, 5])
rdd2 = sc.parallelize([4, 5, 2])
rdd1.intersection(rdd2).collect()
```

---

## reduceByKey()

```python
rdd = sc.parallelize(["A", "B", "B", "D", "A"])
pairs = rdd.map(lambda x: (x, 1))
pairs.reduceByKey(lambda a, b: a + b).collect()
```

---

## groupByKey()

```python
pairs.groupByKey().mapValues(lambda vals: sum(vals)).collect()
```

Note: - reduceByKey is preferred for aggregation because it minimizes
shuffle.

---

## repartition() and coalesce()

```python
rdd = sc.parallelize([10, 20, 30, 40])
rdd2 = rdd.repartition(5)
rdd3 = rdd2.coalesce(2)
```

Use coalesce when reducing partitions to avoid unnecessary shuffle.

---

## Example Complete Pipeline

```python
text_rdd = sc.parallelize(["hello spark", "hello world"])

result = (
    text_rdd
    .flatMap(lambda x: x.split())
    .map(lambda word: (word, 1))
    .reduceByKey(lambda a, b: a + b)
)

result.collect()
```