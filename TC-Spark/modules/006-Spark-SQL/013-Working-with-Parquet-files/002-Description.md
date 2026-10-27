## Introduction to Parquet

Parquet is a columnar storage file format widely used in big data
systems.

Unlike row-based formats (CSV, JSON), Parquet stores data column-wise.

---

## Why Parquet is Important

### 1. Columnar Storage

- Reads only required columns
- Reduces disk I/O
- Improves query performance

---

### 2. Compression & Encoding

- Uses efficient compression
- Type-specific encoding
- Reduces storage space

---

### 3. Schema Storage

- Stores schema along with data
- No need to redefine schema while reading

---

### 4. Predicate Pushdown

Spark can filter data at storage level, improving performance.

---

## Reading and Writing Parquet in Spark

Spark provides built-in support for:

- spark.read.parquet()
- df.write.parquet()

Schema is automatically preserved.

---

## Partitioned Parquet

While writing:

df.write.partitionBy("column").parquet("path")

This creates folder-based partitions on disk.

Example directory structure:

path/ department=Sales/ department=Finance/

Partition pruning improves performance.

---

## Advantages Over JSON/CSV

- Faster reads
- Lower storage size
- Better compression
- Optimized analytics workloads