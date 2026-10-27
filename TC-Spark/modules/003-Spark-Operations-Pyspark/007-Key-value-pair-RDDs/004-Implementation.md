## Step 1: Create Pair RDD

```python
from pyspark import SparkContext

sc = SparkContext("local[*]", "PairRDDExample")

rdd = sc.parallelize(["hello", "hi", "is", "hi", "hello", "hi", "am"])
pairRDD = rdd.map(lambda x: (x, 1))

pairRDD.collect()
```

---

## reduceByKey()

```python
pairRDD.reduceByKey(lambda x, y: x + y).collect()
```

---

## groupByKey()

```python
pairRDD.groupByKey().mapValues(lambda vals: sum(vals)).collect()
```

Note: reduceByKey() is more efficient for aggregation.

---

## aggregateByKey()

```python
pairRDD.aggregateByKey(
    0,
    lambda acc, val: acc + val,
    lambda acc1, acc2: acc1 + acc2
).collect()
```

---

## sortByKey()

```python
pairRDD.distinct().sortByKey().collect()
```

---

## keys() and values()

```python
pairRDD.keys().distinct().collect()

pairRDD.reduceByKey(lambda x, y: x + y).values().collect()
```

---

## collectAsMap()

```python
pairRDD.reduceByKey(lambda x, y: x + y).collectAsMap()
```

---

## countByKey()

```python
pairRDD.countByKey()
```

---

## lookup()

```python
pairRDD.lookup("hi")
```

---

## reduceByKeyLocally()

```python
pairRDD.reduceByKeyLocally(lambda x, y: x + y)
```