### 1. Hadoop MapReduce Example (Conceptual Flow)

In Hadoop MapReduce, developers write:

-   Mapper class
-   Reducer class
-   Driver class

Example (Word Count Logic -- Conceptual):

Mapper: - Input: Line of text - Output: (word, 1)

Reducer: - Input: (word, list_of_counts) - Output: (word, total_count)

Execution Flow: 1. Data stored in HDFS 2. Map phase processes input
splits 3. Shuffle and sort 4. Reduce phase aggregates results 5. Output
written back to HDFS

This requires significant boilerplate code, typically written in Java.

------------------------------------------------------------------------

### 2. Spark Implementation Example (PySpark)

Install PySpark:

``` bash
pip install pyspark
```

Create Spark Session:

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("HadoopVsSparkDemo").getOrCreate()
```

Load Data:

``` python
df = spark.read.text("input.txt")
df.show()
```

Word Count Using Spark:

``` python
from pyspark.sql.functions import explode, split

words = df.select(explode(split(df.value, " ")).alias("word"))

word_counts = words.groupBy("word").count()

word_counts.show()
```

Notice:

-   No manual Map or Reduce functions
-   Minimal code
-   High-level DataFrame API
-   Optimized execution through DAG scheduler

------------------------------------------------------------------------

### 3. Performance Comparison (Practical Understanding)

Hadoop: - Writes intermediate results to disk - Slower for iterative
algorithms

Spark: - Stores intermediate data in memory - Faster for machine
learning and repeated computations

Example Iterative Logic:

``` python
for i in range(5):
    df = df.withColumn("new_col", df.some_column * 2)
```

Spark handles this efficiently due to in-memory processing.

------------------------------------------------------------------------

### 4. Streaming Example (Spark Only)

``` python
stream_df = spark.readStream.format("csv")     .option("header", "true")     .load("stream_folder")

query = stream_df.writeStream     .outputMode("append")     .format("console")     .start()

query.awaitTermination()
```

Hadoop MapReduce does not natively support this.
