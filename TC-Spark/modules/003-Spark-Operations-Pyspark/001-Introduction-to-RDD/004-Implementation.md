## Step 1: Import Required Libraries

``` python
from pyspark import SparkContext, SparkConf
```

## Step 2: Create Spark Configuration and Context

``` python
conf = SparkConf().setMaster("local[*]").setAppName("RDDExample")
sc = SparkContext(conf=conf)
```

Explanation: - local\[\*\] uses all available cores - SparkContext
initializes the Spark execution environment

------------------------------------------------------------------------

## Method 1: Create RDD Using parallelize()

``` python
data = [10, 20, 30, 40, 50]
rdd = sc.parallelize(data)
```

Check partitions:

``` python
rdd.getNumPartitions()
```

------------------------------------------------------------------------

## Method 2: Create RDD from Existing RDD

``` python
rdd1 = sc.parallelize([1, 2, 3])
rdd2 = rdd1.map(lambda x: x + 1)
rdd2.collect()
```

-   map() → Transformation
-   collect() → Action

------------------------------------------------------------------------

## Method 3: Create RDD from External File

``` python
rdd = sc.textFile("data.txt")
```

Each line becomes one element in the RDD.

Common sources: - HDFS - Amazon S3 - Local file system

------------------------------------------------------------------------

## Method 4: Create RDD from DataFrame

``` python
demo_rdd = df.rdd
```

Converts structured data into an RDD of Row objects.

------------------------------------------------------------------------

# Transformations vs Actions

## Transformations (Lazy)

-   map()
-   filter()
-   flatMap()
-   reduceByKey()
-   distinct()

## Actions (Trigger Execution)

-   collect()
-   count()
-   take()
-   first()
-   saveAsTextFile()

Transformations build a DAG; actions execute it.