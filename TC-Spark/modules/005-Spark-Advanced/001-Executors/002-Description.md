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