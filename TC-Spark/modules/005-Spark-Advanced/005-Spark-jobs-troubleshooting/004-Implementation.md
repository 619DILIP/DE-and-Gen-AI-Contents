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