<details><summary>Learning Objectives</summary>

After completing this module, associates should be able to:

- Define the Spark Driver
- Explain the responsibilities of the Driver
- Understand how the Driver coordinates distributed execution
- Identify important driver configuration parameters
- Diagnose driver-related performance issues
- Configure driver memory and cores appropriately

</details>

<details><summary>Description</summary>

## What is the Spark Driver?

The Spark Driver is the central coordinator of a Spark application.

When a Spark application is submitted:

1.  The Driver process starts.
2.  The main() function of the program executes inside the Driver.
3.  SparkSession or SparkContext is created.
4.  The Driver communicates with the Cluster Manager to request resources.
5.  Executors are launched on worker nodes.
6.  The Driver schedules tasks and monitors execution.

The Driver is responsible for orchestrating the entire distributed
workflow.

---

## Responsibilities of the Driver

### 1. Application Entry Point

- Executes the main() program logic.
- Initializes SparkSession / SparkContext.

---

### 2. Logical and Physical Planning

- Builds logical plan from user code.
- Optimizes execution plan.
- Converts plan into stages and tasks.

---

### 3. Task Scheduling

- Divides jobs into stages.
- Breaks stages into tasks.
- Distributes tasks to executors.

---

### 4. Resource Coordination

- Requests resources from cluster manager.
- Determines number of executors.
- Tracks executor health.

---

### 5. Result Aggregation

- Collects results from executors.
- Sends final output to client.

---

### 6. Metadata Tracking

- Tracks cached RDDs/DataFrames.
- Maintains DAG execution lineage.

---

## Important Driver Configuration Parameters

### spark.driver.memory

- Memory allocated to the driver process.
- Default: 1 GB
- Increase when:
  - Using collect()
  - Large broadcast variables
  - Large joins
  - Machine learning workflows

---

### spark.driver.cores

- Number of CPU cores allocated to the driver.
- Important for:
  - Heavy scheduling workloads
  - Complex DAG planning
  - Multiple concurrent jobs

---

## Common Driver Issues

- Driver OutOfMemoryError
- Excessive collect() usage
- Driver becoming bottleneck
- Large broadcast variable failures

Proper configuration prevents driver failures.

</details>

<details><summary>Real World Application</summary>

## 1. Interactive Analytics

Data scientists frequently use collect() or show(). If driver memory is
insufficient → crashes.

Solution: Increase spark.driver.memory.

---

## 2. Machine Learning Model Training

Driver coordinates iterative training. Large metadata and model states
stored in driver.

Solution: Increase driver memory and cores.

---

## 3. Large Broadcast Variables

Broadcasting large datasets from driver to executors requires sufficient
driver memory.

---

## 4. Streaming Applications

Driver handles micro-batch scheduling. Under-provisioned driver →
scheduling delays.

---

</details>

<details><summary>Implementation</summary>

## Configuring Driver Using spark-submit

```bash
spark-submit   --master yarn   --deploy-mode cluster   --driver-memory 4G   --driver-cores 2   script_name.py
```

---

## Configuring Driver Inside Application

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("DriverConfigExample")
    .config("spark.driver.memory", "4g")
    .config("spark.driver.cores", "2")
    .getOrCreate()
)
```

---

## Example: Driver Memory Issue

Bad practice:

```python
large_df.collect()
```

Better approach:

```python
large_df.limit(100).show()
```

---

## Monitoring Driver

1.  Open Spark UI
2.  Check Driver Logs
3.  Monitor memory usage
4.  Identify bottlenecks

---

## Stopping Spark Application

```python
spark.stop()
```

This releases all cluster resources.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- The Driver is the central coordinator of Spark applications.
- It executes the main() function.
- It creates execution plans and schedules tasks.
- It communicates with cluster manager and executors.
- It aggregates results from executors.
- Two critical parameters:
  - spark.driver.memory
  - spark.driver.cores
- Proper driver configuration ensures stability and performance.

Understanding the Driver is essential for building scalable distributed Spark systems.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
