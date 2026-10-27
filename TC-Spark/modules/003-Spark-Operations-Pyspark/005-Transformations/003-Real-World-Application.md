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