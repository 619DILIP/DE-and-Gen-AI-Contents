<details><summary>Learning Overview</summary>

After Completing This Module, You Will Be Able To:

-   Differentiate between transformations and actions
-   Explain lazy evaluation in the context of RDD operations
-   Distinguish between narrow and wide transformations
-   Understand how shuffling impacts performance
-   Identify when Spark triggers execution
-   Apply RDD operations effectively in real-world scenarios

</details>

<details><summary> Description </summary>

RDDs support two major types of operations:

1.  Transformations
2.  Actions

These operations define how data flows and how computation is executed
within Spark.

------------------------------------------------------------------------

## Transformations

Transformations are operations that:

-   Manipulate data inside an RDD
-   Return a new RDD
-   Are evaluated lazily
-   Build a lineage graph (DAG)

Transformations do not execute immediately. Instead, Spark records them
and waits for an action to trigger execution.

### Example

``` python
rdd2 = rdd1.map(lambda x: x * 2)
```

Here, a new RDD is created, but computation does not start yet.

------------------------------------------------------------------------

## Types of Transformations

Transformations are categorized into:

### 1. Narrow Transformations

In a narrow transformation:

-   Each output partition depends on only one parent partition
-   No data movement occurs between partitions
-   No shuffling happens

Examples:

-   map()
-   flatMap()
-   filter()
-   union()
-   mapPartitions()

Narrow transformations are more efficient because they avoid network
communication.

------------------------------------------------------------------------

### 2. Wide Transformations

In a wide transformation:

-   Output partitions depend on multiple parent partitions
-   Data is redistributed across partitions
-   Shuffling occurs

Shuffling is expensive because it involves network communication and
disk I/O.

Examples:

-   groupByKey()
-   reduceByKey()
-   aggregateByKey()
-   join()
-   repartition()

Wide transformations are more costly than narrow transformations.

------------------------------------------------------------------------

## Actions

Actions are operations that:

-   Trigger execution of all transformations
-   Return a non-RDD value
-   Store results in the driver program or external storage

Examples:

-   count()
-   collect()
-   first()
-   take()
-   reduce()
-   saveAsTextFile()

Example:

``` python
rdd2.collect()
```

This triggers execution of all previously defined transformations.

</details>

<details><summary> Real World Application </summary>

Understanding RDD operations is critical in real-world scenarios such
as:

## Log Analysis

-   filter() to extract error logs
-   map() to format log entries
-   count() to compute total errors

## Word Count Application

-   flatMap() to split lines into words
-   map() to assign count 1 to each word
-   reduceByKey() to aggregate word frequencies

## Data Aggregation

-   groupByKey() or reduceByKey() to compute totals
-   collect() or saveAsTextFile() to retrieve final results

Choosing narrow transformations when possible improves performance.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

-   RDD operations are categorized into Transformations and Actions
-   Transformations return a new RDD and are evaluated lazily
-   Actions trigger execution and return non-RDD values
-   Transformations can be narrow or wide
-   Wide transformations involve shuffling and are more expensive
-   Understanding these operations is essential for writing efficient Spark programs

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>