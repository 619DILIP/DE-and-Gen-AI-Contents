<details><summary> Learning Objectives </summary>

After completing this module, learners will be able to:

-   Load data from different filesystems into an RDD
-   Understand how textFile() and wholeTextFiles() work
-   Control partitions while loading data
-   Save RDD results back to storage
-   Understand how Spark stores output files

</details>

<details><summary> Description </summary>

In distributed data processing, loading and saving data efficiently is
critical. Spark provides flexible methods to read data from multiple
storage systems and write processed results back.

RDD (Resilient Distributed Dataset) is Spark's fundamental data
abstraction. It allows distributed processing of data across clusters.

Spark supports reading from:

-   Local filesystem
-   HDFS
-   Amazon S3
-   Other distributed storage systems

------------------------------------------------------------------------

## Loading Data into RDD

Spark provides two main methods for reading files into an RDD:

### 1. textFile()

Reads a file as a collection of lines.

Syntax:

``` python
sc.textFile("path")
```

Key Features:

-   Reads single or multiple files
-   Supports wildcards
-   Works with local, HDFS, and S3
-   Allows optional partition count

Example:

``` python
rdd = sc.textFile("/data/demo.txt")
```

Specify partitions:

``` python
rdd = sc.textFile("/data/demo.txt", 4)
```

------------------------------------------------------------------------

### 2. wholeTextFiles()

Reads entire files and returns (filename, content) pairs.

Syntax:

``` python
sc.wholeTextFiles("path")
```

Example:

``` python
rdd = sc.wholeTextFiles("/data/")
```

Output format:

(filename, file_content)

This is useful when processing entire documents instead of line-by-line
data.

------------------------------------------------------------------------

## Saving RDD to Filesystem

After transformations, Spark allows saving results using:

### saveAsTextFile()

Syntax:

``` python
rdd.saveAsTextFile("path")
```

Spark automatically creates partition files:

part-00000\
part-00001\
part-00002

Each file contains part of the distributed dataset.

</details>

<details><summary> Real World Application </summary>

### 1. Log Processing Systems

Companies load server logs using textFile() to:

-   Parse log entries
-   Extract metrics
-   Detect anomalies

Processed logs are saved back to HDFS or cloud storage.

------------------------------------------------------------------------

### 2. Document Processing

wholeTextFiles() is used when:

-   Processing research papers
-   Handling legal documents
-   Analyzing articles

Each file is treated as a single record.

------------------------------------------------------------------------

### 3. Data Pipelines

In production systems:

1.  Load raw data from S3 or HDFS
2.  Apply transformations
3.  Save cleaned output to another location
4.  Downstream systems consume the processed data

RDD file operations form the backbone of ETL pipelines.

</details>

<details><summary> Implementation </summary>

## Step 1: Create SparkContext

``` python
from pyspark import SparkContext

sc = SparkContext("local[*]", "RDDFileExample")
```

------------------------------------------------------------------------

## Step 2: Reading Files

### Local File

``` python
rdd1 = sc.textFile("/abc/xyz/demo.txt")
```

### With Partition Count

``` python
rdd1 = sc.textFile("/abc/xyz/demo.txt", 4)
```

### Multiple Files (Wildcard)

``` python
rdd1 = sc.textFile("/abc/xyz/*")
```

### HDFS File

``` python
rdd1 = sc.textFile("hdfs://abc/xyz/demo.txt")
```

### Amazon S3 File

``` python
rdd1 = sc.textFile("s3a://abc/xyz/demo.txt")
```

------------------------------------------------------------------------

## Using wholeTextFiles()

``` python
rdd1 = sc.wholeTextFiles("/abc/xyz/")
```

------------------------------------------------------------------------

## Step 3: Saving Output

### Local Filesystem

``` python
rdd1.saveAsTextFile("/abc/output")
```

### HDFS

``` python
rdd1.saveAsTextFile("hdfs://abc/output")
```

### Amazon S3

``` python
rdd1.saveAsTextFile("s3a://abc/output")
```

------------------------------------------------------------------------

## Important Notes

-   Output directory must NOT already exist.
-   Spark creates multiple part files.
-   Number of part files = number of partitions.
-   Use rdd.coalesce() or rdd.repartition() to control output file count.

Example:

``` python
rdd1.coalesce(1).saveAsTextFile("/abc/output_single")
```
</details>

<details><summary> Summary </summary>

In this module, we learned:

-   How to load files into RDD using textFile() and wholeTextFiles()
-   How to read from local, HDFS, and S3
-   How to save processed data using saveAsTextFile()
-   How Spark generates partition-based output files
-   How these operations are used in real-world ETL and analytics pipelines

RDD file operations are fundamental building blocks in distributed data
processing systems.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>