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
-   Use rdd.coalesce() or rdd.repartition() to control output file
    count.

Example:

``` python
rdd1.coalesce(1).saveAsTextFile("/abc/output_single")
```
