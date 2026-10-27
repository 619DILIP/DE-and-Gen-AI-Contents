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