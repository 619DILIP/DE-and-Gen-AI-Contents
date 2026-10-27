<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Understand the role of Driver and Executors in Spark architecture
- Configure executor cores and instances correctly
- Calculate optimal executor memory allocation
- Configure driver memory and cores
- Apply memory configuration during spark-submit
- Optimize Spark job performance through resource tuning

</details>

<details><summary> Description </summary>

In a distributed Spark application, performance heavily depends on how
the Driver and Executors are configured.

Improper configuration can lead to:

- OutOfMemory errors
- Underutilized cluster resources
- Excessive garbage collection
- Poor parallelism
- Increased shuffle time

To optimize Spark jobs, the following configurations are critical:

- spark.executor.cores
- spark.executor.instances
- spark.executor.memory
- spark.driver.memory
- spark.driver.cores

---

## Key Configuration Parameters

### 1. spark.executor.cores

Defines the number of CPU cores per executor.

- Default: 1
- Recommended: 3--5 cores per executor
- Avoid very high values (too many cores reduce parallelism and
  increase GC overhead)

Best Practice: Keep executors small and balanced rather than very large.

---

### 2. spark.executor.instances

Defines total number of executors in the cluster.

Formula:

Number of Executors = Total Available Cores / spark.executor.cores

Where:

Total Available Cores = (Nodes × Cores per Node) − Reserved Cores

---

### 3. spark.executor.memory

Defines memory allocated per executor.

Formula:

Executor Memory = (RAM per Node / Executors per Node) − Memory Overhead

Memory overhead is typically:

max(384MB, 10% of executor memory)

---

### 4. spark.driver.cores

Number of cores allocated to the driver process.

- Often set equal to executor cores for balance
- Increase for large scheduling workloads

---

### 5. spark.driver.memory

Memory allocated to the driver.

- Should be sufficient for collecting results
- Increase when using collect(), broadcast variables, or large
  aggregations

</details>

<details><summary> Real World Application </summary>

## 1. Large-Scale ETL Jobs

When processing terabytes of data:

- Increase executor.instances
- Use moderate executor.cores (3--5)
- Allocate memory based on shuffle requirements

---

## 2. Machine Learning Workloads

ML pipelines require:

- Higher executor memory
- Balanced core allocation
- Increased driver memory for model coordination

---

## 3. Streaming Applications

For streaming workloads:

- Smaller executors
- More instances
- Avoid memory bottlenecks
- Maintain low latency

---

Proper tuning directly impacts job completion time, cluster efficiency,
and cost optimization in cloud environments.

</details>

<details><summary> Implementation </summary>

## Cluster Assumptions

Let us consider a cluster with:

- 10 Nodes
- 16 Cores per Node
- 64 GB RAM per Node

---

## Step 1: Reserve System Resources

Reserve 1 core per node for system daemons.

Available cores per node:

16 − 1 = 15 cores

Total available cores:

15 × 10 = 150 cores

---

## Step 2: Choose Executor Cores

Set:

spark.executor.cores = 5

---

## Step 3: Calculate Number of Executors

Number of Executors:

150 / 5 = 30

Executors per node:

30 / 10 = 3

Reserve 1 executor for Application Manager:

spark.executor.instances = 29

---

## Step 4: Calculate Executor Memory

Executors per node = 3

Memory per executor:

64 GB / 3 ≈ 21.33 GB

Memory overhead (10%):

2.13 GB

Actual executor memory:

21.33 − 2.13 ≈ 19 GB

Final configuration:

spark.executor.memory = 19G

---

## Step 5: Configure Driver

Recommended:

spark.driver.cores = 5\
spark.driver.memory = 19G

Adjust based on workload requirements.

---

## Submitting Spark Job with Configuration

Example:

```bash
spark-submit   --master yarn   --deploy-mode cluster   --executor-cores 5   --executor-instances 29   --executor-memory 19G   --driver-cores 5   --driver-memory 19G   script_name.py
```

---

## Alternative: Configure Inside Application

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("MemoryConfigExample")
    .config("spark.executor.cores", "5")
    .config("spark.executor.instances", "29")
    .config("spark.executor.memory", "19g")
    .config("spark.driver.memory", "19g")
    .getOrCreate()
)
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Driver and Executors control distributed computation
- Proper resource allocation improves performance
- spark.executor.cores controls parallelism
- spark.executor.instances controls total executors
- spark.executor.memory must account for overhead
- Driver memory must support result aggregation
- Resource tuning is workload dependent

Correct configuration ensures maximum cluster utilization, minimal failures, and optimal performance in distributed Spark jobs.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
