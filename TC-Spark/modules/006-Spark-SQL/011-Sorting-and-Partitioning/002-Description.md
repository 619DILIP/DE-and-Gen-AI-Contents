## Introduction to Partitioning

Partitioning in Spark refers to dividing a dataset into smaller logical
chunks called partitions.

Each partition:

- Is processed in parallel
- Resides on a single executor
- Corresponds to one task during execution

Proper partitioning improves:

- Parallelism
- Resource utilization
- Performance

---

## Default Partitioning Behavior

### Local Mode

When running in local mode:

The number of partitions typically equals the number of cores specified
in:

spark = SparkSession.builder.master("local\[5\]").getOrCreate()

This creates 5 parallel partitions.

---

### Cluster Mode

In distributed clusters:

Partitions are influenced by:

- HDFS block size
- Total executor cores
- spark.sql.shuffle.partitions (default 200)

For example:

If HDFS block size is 128 MB and file size is 640 MB:

640 / 128 = 5 partitions

---

## Repartition vs Coalesce

### repartition()

- Increases or decreases partitions
- Causes full shuffle
- Expensive operation

### coalesce()

- Reduces partitions
- Avoids full shuffle (when decreasing)
- More efficient for reducing partitions

---

## Partitioning While Writing Data

Use partitionBy():

df.write.partitionBy("column_name").parquet("output_path")

This creates folder-based partitioning on disk.

---

## Introduction to Sorting

Sorting arranges data in ascending or descending order.

Spark provides:

- sort()
- orderBy()
- asc()
- desc()
- asc_nulls_first()
- desc_nulls_last()

Sorting triggers shuffle when applied globally.

---

## Global vs Local Sorting

- orderBy() → Global sort (shuffle required)
- sortWithinPartitions() → Sort inside each partition only

---

## Performance Considerations

- Sorting large datasets can be expensive
- Repartitioning unnecessarily increases shuffle
- Proper partition size improves efficiency
- Default shuffle partitions = 200