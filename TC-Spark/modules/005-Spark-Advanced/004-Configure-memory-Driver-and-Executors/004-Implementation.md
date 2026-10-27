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