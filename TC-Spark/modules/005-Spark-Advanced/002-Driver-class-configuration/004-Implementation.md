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