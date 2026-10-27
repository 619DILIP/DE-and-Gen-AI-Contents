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