<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Understand RDD immutability
- Explain lazy evaluation and DAG execution
- Differentiate between narrow and wide transformations
- Apply common RDD transformations correctly
- Optimize transformations for performance
- Control partitioning strategies
- Avoid common performance pitfalls
- Design scalable RDD pipelines

</details>

<details><summary>Description</summary>

RDD Transformations are operations that create a new RDD from an
existing RDD.

Key Properties:

- RDDs are immutable (original data is never modified).
- Transformations are lazy (execution happens only after an action).
- Spark builds a Directed Acyclic Graph (DAG) of transformations.
- Execution is optimized before running.

## Types of Transformations

### 1. Narrow Transformations

- No data shuffle required
- Faster execution
- Data stays within partitions

Examples: - map() - filter() - flatMap() - mapValues()

### 2. Wide Transformations

- Require shuffle across partitions
- More expensive operations
- Network communication involved

Examples: - groupByKey() - reduceByKey() - distinct() - repartition() -
intersection() - sortBy()

Choosing the correct transformation directly impacts performance.

</details>

<details><summary>Real World Application</summary>

### Log Aggregation System

1.  Load logs
2.  filter() error logs
3.  map() extract fields
4.  reduceByKey() count error types
5.  saveAsTextFile() store results

---

### Word Count Pipeline

1.  flatMap() split words
2.  map() create (word,1)
3.  reduceByKey() count words

Classic distributed example.

---

### Data Deduplication

1.  union() combine datasets
2.  distinct() remove duplicates
3.  repartition() optimize output
4.  save results

---

## Performance Considerations

1.  Avoid groupByKey for aggregation.
2.  Minimize wide transformations.
3.  Control partitions before writing output.
4.  Chain narrow transformations efficiently.
5.  Use caching (persist()) for reused RDDs.

Example:

```python
rdd.persist()
```

---

## DAG Execution Example

Example Pipeline:

```python
rdd = sc.textFile("data.txt")
words = rdd.flatMap(lambda x: x.split())
pairs = words.map(lambda word: (word, 1))
counts = pairs.reduceByKey(lambda a,b: a+b)
counts.collect()
```

Spark builds DAG first → Executes only when collect() runs.

---

</details>

<details><summary> Implementation </summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- RDD transformations create new RDDs
- Transformations are lazily evaluated
- Narrow vs wide transformations
- Key-value transformations
- Partition control strategies
- Performance optimization techniques
- Real-world ETL and analytics use cases

Understanding transformations is fundamental for writing scalable,
efficient distributed Spark applications.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
