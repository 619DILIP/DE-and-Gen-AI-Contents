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