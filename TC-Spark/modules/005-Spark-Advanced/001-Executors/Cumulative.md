<details><summary> Learning Objectives</summary>

After completing this module, learners will be able to:

- Understand what Spark Executors are
- Explain the role of executors in distributed execution
- Understand how executors interact with the driver
- Identify key executor configuration parameters
- Understand executor lifecycle
- Optimize executor configuration for better performance

</details>

<details><summary> Description </summary>

In Apache Spark, Executors are distributed worker processes responsible
for executing tasks assigned by the Driver.

When a Spark application starts:

1.  The Driver requests resources from the Cluster Manager.
2.  The Cluster Manager launches Executors on worker nodes.
3.  Executors register themselves with the Driver.
4.  The Driver assigns tasks to Executors.
5.  Executors execute tasks and return results.

Executors are application-specific. When the application finishes,
executors are terminated.

---

## Responsibilities of Executors

### 1. Task Execution

- Run tasks sent by the driver
- Execute transformations and actions
- Process partitions in parallel

---

### 2. Data Storage

- Cache and persist RDDs or DataFrames in memory
- Spill data to disk if necessary
- Manage execution and storage memory

---

### 3. Shuffle Operations

- Write shuffle data to disk
- Fetch shuffle data from other executors
- Participate in distributed aggregation

---

### 4. Communication

- Communicate directly with the driver
- Send status updates and results
- Report failures

---

## Executor Lifecycle

1.  Application starts
2.  Driver requests resources
3.  Cluster Manager launches Executors
4.  Executors register with Driver
5.  Tasks are scheduled
6.  Executors execute tasks
7.  Application completes
8.  Executors shut down

Executors are not shared across applications.

---

## Important Executor Configuration Parameters

### spark.executor.cores

- Number of CPU cores per executor
- Controls number of parallel tasks per executor
- Recommended: 3--5 cores

---

### spark.executor.instances

- Total number of executors
- Controls parallelism across cluster
- Based on total cluster cores

---

### spark.executor.memory

- Memory allocated per executor
- Used for:
  - Task execution
  - Caching
  - Shuffle buffers
- Must account for memory overhead

</details>

<details><summary> Real World Application </summary>

## 1. Large Batch ETL

- Multiple executors process data partitions in parallel
- Proper executor sizing reduces job completion time

---

## 2. Machine Learning Training

- Executors process training data partitions
- Larger executor memory improves caching performance

---

## 3. Streaming Applications

- Executors process streaming micro-batches
- Balanced executor cores prevent latency spikes

---

## 4. Cloud Cost Optimization

- Over-provisioned executors waste resources
- Under-provisioned executors increase job runtime
- Proper tuning reduces infrastructure cost

</details>

<details><summary> Implementation </summary>

## Creating Spark Session

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("ExecutorExample")
    .config("spark.executor.cores", "4")
    .config("spark.executor.instances", "8")
    .config("spark.executor.memory", "8g")
    .getOrCreate()
)
```

---

## Submitting Job with Executor Configuration

```bash
spark-submit   --master yarn   --deploy-mode cluster   --executor-cores 4   --executor-instances 8   --executor-memory 8G   script_name.py
```

---

## Checking Executors in Spark UI

After submitting the job:

1.  Open Spark Web UI
2.  Navigate to Executors tab
3.  Observe:
    - Executor ID
    - Host
    - Memory usage
    - Storage memory
    - Active tasks

---

## Example: Parallel Processing

```python
rdd = spark.sparkContext.parallelize(range(1000), 8)

result = rdd.map(lambda x: x * 2).collect()
```

Here:

- 8 partitions
- Executors process partitions in parallel
- More executors → higher parallelism

</details>

<details><summary> Summary </summary>

In this module, we learned:

- Executors are worker processes in Spark
- They execute tasks and return results to the driver
- They cache data and manage shuffle operations
- They are application-specific
- Key parameters include:
  - spark.executor.cores
  - spark.executor.instances
  - spark.executor.memory
- Proper executor configuration improves performance and efficiency

Understanding Executors is fundamental to tuning Spark applications for scalability and performance.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
