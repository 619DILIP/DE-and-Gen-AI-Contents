<details><summary>Learning Objectives </summary>

After completing this module, learners will be able to:

- Understand what a Key-Value Pair RDD is
- Create pair RDDs from existing RDDs
- Apply transformation operations specific to pair RDDs
- Apply action operations specific to pair RDDs
- Choose efficient aggregation strategies
- Design scalable key-based distributed computations

</details>

<details><summary> Description </summary>

A Key-Value Pair RDD (also called Pair RDD) is an RDD where each element
is stored as a tuple:

(key, value)

Pair RDDs are powerful because Spark provides specialized operations
that operate on keys efficiently. These operations are heavily used in
aggregation, grouping, and distributed computation pipelines.

Pair RDDs are commonly used in:

- Word count problems
- Log aggregation
- Event counting
- Data grouping and summarization
- Distributed joins

---

## Transformations on Pair RDDs

### reduceByKey()

- Aggregates values for each key.
- Performs map-side combine (more efficient).
- Preferred for aggregation.

---

### groupByKey()

- Groups all values for each key.
- Causes full shuffle.
- Less efficient for aggregation compared to reduceByKey().

---

### aggregateByKey()

- Similar to reduceByKey().
- Allows different input and output types.
- Useful for advanced aggregation logic.

---

### sortByKey()

- Sorts data by key.
- Can be ascending or descending.
- Causes shuffle.

---

### sampleByKey()

- Returns a sampled subset of keys.
- Useful in statistical analysis.

---

### mapValues()

- Applies transformation only to values.
- Does not change keys.
- Narrow transformation.

---

### keys() and values()

- keys() → returns RDD containing only keys.
- values() → returns RDD containing only values.

---

## Actions on Pair RDDs

### collectAsMap()

- Returns result as a dictionary.
- Suitable for small datasets only.

---

### countByKey()

- Counts number of elements for each key.
- Returns result to driver.

---

### lookup(key)

- Returns list of values associated with a key.

---

### reduceByKeyLocally()

- Aggregates values by key and returns result to driver.

</details>

<details><summary> Real World Application </summary>

## 1. Word Count System

- Convert words into (word, 1)
- Use reduceByKey() to count occurrences
- Save aggregated results

---

## 2. Log Analytics

- Extract (error_code, 1)
- Use reduceByKey() to count error frequency
- Use sortByKey() to organize logs

---

## 3. Sales Aggregation

- Create (product_id, sale_amount)
- Use aggregateByKey() to compute total revenue
- Use keys() to get unique product IDs

---

## 4. Data Sampling

- Use sampleByKey() to analyze subset of large datasets

Efficient key-based transformations are critical in distributed systems
where aggregation is common.

</details>

<details><summary> Implementation </summary>

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

</details>

<details><summary> Summary </summary>

In this module, we learned:

- Pair RDDs store data as (key, value) tuples
- Spark provides specialized transformations for key-based aggregation
- reduceByKey() is preferred over groupByKey() for performance
- aggregateByKey() allows flexible aggregation logic
- keys(), values(), and mapValues() help manipulate key-value data
- Pair RDDs are essential for distributed aggregation pipelines

Understanding Pair RDDs is fundamental for building scalable distributed analytics systems.
    
</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
