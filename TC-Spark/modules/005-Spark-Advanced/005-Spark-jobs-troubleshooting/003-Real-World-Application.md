## Issue 1: Spark YARN Jobs Do Not Start

Symptom: - Job stuck in ACCEPTED state - Resource Manager shows errors

Cause: - Insufficient cluster resources - Incorrect configuration

Solution: - Reduce executor memory - Reduce executor instances - Check
YARN Resource Manager logs

---

## Issue 2: Job Repeatedly Fails

Symptom: - Application retries multiple times - Executors lost

Cause: - Memory pressure - Data skew - Misconfigured resources

Solution: - Analyze Spark UI for skew - Repartition data - Adjust
executor memory

---

## Issue 3: S3 Throttling Errors

Symptom: - Slow writes - Multipart upload failures

Cause: - High request rate - AWS throttling

Solution: - Tune spark.hadoop.fs.s3a.connection.maximum - Increase
multipart size - Optimize write partitions

---

## Issue 4: Job Extremely Slow

Symptom: - Stages taking long time - Few tasks running

Cause: - Too few partitions - Improper executor configuration

Solution: - Increase parallelism - Use repartition() - Adjust
spark.sql.shuffle.partitions