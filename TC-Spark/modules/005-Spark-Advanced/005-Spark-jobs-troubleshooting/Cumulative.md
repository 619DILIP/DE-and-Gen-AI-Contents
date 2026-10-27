<details><summary>Learning Objectives</summary>

After completing this module, associates should be able to:

- Define what a Spark job is
- Understand Spark job lifecycle
- Identify common Spark job failures
- Diagnose Spark job errors using logs and Spark UI
- Troubleshoot resource, memory, and configuration issues
- Apply systematic debugging strategies in distributed environments

</details><details><summary>Description</summary>

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

</details><details><summary>Real World Application</summary>

## Issue 1: Spark YARN Jobs Do Not Start

Symptom: - Job stuck in ACCEPTED state - Resource Manager shows errors

Cause: - Insufficient cluster resources - Incorrect configuration

Solution: - Reduce executor memory - Reduce executor instances - Check
YARN Resource Manager logs

---

## Issue 2: Job Repeatedly Fails

Symptom: - Application retries multiple times - Executors lost

Cause: - Memory pressure - Data skew - Misconfigured resources

Solution: - Analyze Spark UI for skew - Repartition data - Adjust
executor memory

---

## Issue 3: S3 Throttling Errors

Symptom: - Slow writes - Multipart upload failures

Cause: - High request rate - AWS throttling

Solution: - Tune spark.hadoop.fs.s3a.connection.maximum - Increase
multipart size - Optimize write partitions

---

## Issue 4: Job Extremely Slow

Symptom: - Stages taking long time - Few tasks running

Cause: - Too few partitions - Improper executor configuration

Solution: - Increase parallelism - Use repartition() - Adjust
spark.sql.shuffle.partitions

</details>

<details><summary>Implementation</summary>

## 1. Checking Spark UI

After submitting job:

1.  Open Spark UI (http://driver-node:4040)
2.  Check:
    - Failed Stages
    - Skipped Tasks
    - Executor Loss
    - Shuffle Read/Write size

---

## 2. Example: Memory Issue

Error Example: OutOfMemoryError: Java heap space

Fix by increasing memory:

```bash
spark-submit   --executor-memory 8G   --driver-memory 4G   script_name.py
```

---

## 3. Example: Data Skew Detection

```python
rdd = spark.sparkContext.textFile("data.txt")
pairs = rdd.map(lambda x: (x.split(",")[0], 1))

pairs.countByKey()
```

If one key has extremely high count → skew exists.

Solution: - Salting keys - Repartitioning data

---

## 4. Checking Executor Logs

YARN:

```bash
yarn logs -applicationId <application_id>
```

Standalone:

Check worker node logs under \$SPARK_HOME/work/

---

## 5. Handling Collect() Failures

Bad Practice:

```python
large_df.collect()
```

Better:

```python
large_df.limit(100).show()
```

---

## 6. Restarting Services

If encountering: - closed SQLContext - Thrift server errors

Restart relevant Spark services.

</details><details><summary>Summary</summary>

In this module, we learned:

- Spark jobs are triggered by actions
- Each job consists of stages and tasks
- Most failures occur due to resource misconfiguration
- Spark UI is the primary troubleshooting tool
- Logs provide detailed error information
- Memory tuning and partition management resolve most issues
- Systematic debugging improves reliability of Spark applications

Effective troubleshooting ensures stable, scalable distributed processing.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
