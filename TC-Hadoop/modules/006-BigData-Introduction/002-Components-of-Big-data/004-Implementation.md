## High-Level Component Selection

When designing a Big Data solution, different components are selected according to the requirements.

### Storage Requirement

If the system needs distributed storage for large datasets, a technology such as HDFS can be used.

### Batch Processing Requirement

If large datasets need to be processed as batches, Hadoop MapReduce can be used.

### Fast Distributed Processing Requirement

If the system requires distributed processing for analytics and other workloads, Apache Spark can be used.

### Python-Based Processing Requirement

If developers prefer Python for Spark-based processing, PySpark can be used.

---

## Example Component Selection

Consider an organization that needs to process large amounts of sales data.

A simplified technology selection could be:

```text
Large Sales Dataset
        ↓
      HDFS
        ↓
  Apache Spark
        ↓
     PySpark
        ↓
     Analysis
```
