## Step 1: Setup

``` python
from pyspark import SparkContext, SparkConf

conf = SparkConf().setMaster("local[*]").setAppName("BasicRDDOps")
sc = SparkContext(conf=conf)
```

------------------------------------------------------------------------

## Example 1: Narrow Transformation

``` python
rdd = sc.parallelize([1, 2, 3, 4, 5])
rdd2 = rdd.map(lambda x: x * 2)
rdd2.collect()
```

-   map() is a narrow transformation
-   No shuffling occurs
-   collect() triggers execution

------------------------------------------------------------------------

## Example 2: Wide Transformation

``` python
rdd = sc.parallelize([("a",1), ("b",1), ("a",1)])
rdd2 = rdd.reduceByKey(lambda x, y: x + y)
rdd2.collect()
```

-   reduceByKey() is a wide transformation
-   Shuffling occurs
-   Data is redistributed across partitions

------------------------------------------------------------------------

## Example 3: Action Only

``` python
rdd = sc.parallelize([10, 20, 30])
count_value = rdd.count()
```

count() is an action that triggers execution.

------------------------------------------------------------------------

# 5. Performance Considerations

-   Prefer narrow transformations when possible
-   Minimize shuffling
-   Use reduceByKey() instead of groupByKey() when aggregating
-   Cache RDDs if reused multiple times