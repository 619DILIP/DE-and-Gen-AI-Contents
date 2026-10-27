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