## What is a Spark Job?

A Spark job is triggered whenever an action (such as collect(), count(),
save()) is executed on an RDD or DataFrame.

A Spark Application may contain: - Multiple Jobs - Each job contains
Stages - Each stage contains Tasks

Job Execution Flow:

Driver → Job → Stage → Task → Executor → Result

---

## Common Reasons for Spark Job Failures

### 1. Resource Exhaustion

- Insufficient executor memory
- Insufficient CPU cores
- Cluster fully utilized

### 2. Shuffle Failures

- Large data skew
- Network congestion
- Executor lost during shuffle

### 3. Compilation / Syntax Errors

- Python syntax errors
- Incorrect imports
- Version incompatibilities

### 4. OutOfMemory Errors

- Large collect() operations
- Excessive caching
- Large broadcast variables

### 5. Data Source Failures

- S3 throttling
- HDFS unavailable
- Incorrect file paths

---

## Where to Look When a Job Fails

1.  Spark Driver Logs\
2.  Executor Logs\
3.  Spark UI (Jobs, Stages, Storage tabs)\
4.  Cluster Manager Logs (YARN / Standalone / Kubernetes)

Always start with the first error in the logs.