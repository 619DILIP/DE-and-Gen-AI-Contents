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