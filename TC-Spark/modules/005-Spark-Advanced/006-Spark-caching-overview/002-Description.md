## What is Spark Caching?

Spark Caching is a mechanism used to store intermediate computation
results in memory (or disk) so that they can be reused without
recomputation.

When we call:

- cache()
- persist()

on an RDD or DataFrame, Spark marks that dataset for storage after the
first action is triggered.

Important:

- Caching is lazy.
- Data is cached only after the first action executes.
- It improves performance when the same dataset is reused multiple
  times.

---

## Why Spark Caching is Important

Spark follows a lazy evaluation model. Every time an action is
triggered, Spark recomputes the entire lineage unless the intermediate
result is cached.

Without caching:

Data → Transformations → Action\
(recomputed every time)

With caching:

Data → Transformations → Cached Result → Multiple Actions\
(no recomputation)

---

## When to Use Spark Cache

Use caching when:

- A DataFrame or RDD is reused multiple times
- Multiple actions are applied on the same dataset
- Iterative algorithms (e.g., Machine Learning)
- Complex transformations that are expensive
- ETL pipelines where intermediate results are reused

Avoid caching when:

- Dataset is used only once
- Dataset is too large for available memory
- Recomputing is cheaper than storing

---

## cache() vs persist()

### cache()

Equivalent to:

persist(StorageLevel.MEMORY_ONLY)

Stores data in memory only.

---

### persist()

Allows specifying storage level:

Examples:

- MEMORY_ONLY
- MEMORY_AND_DISK
- DISK_ONLY
- MEMORY_ONLY_SER
- MEMORY_AND_DISK_SER

Example:

```python
from pyspark import StorageLevel
df.persist(StorageLevel.MEMORY_AND_DISK)
```

---

## How Spark Cache Works Internally

1.  cache() marks dataset as cacheable.
2.  First action triggers execution.
3.  Spark stores partitions in executor memory.
4.  Subsequent actions reuse cached partitions.
5.  Cache Manager tracks cached datasets.

Cached data resides in executor memory, not driver memory.