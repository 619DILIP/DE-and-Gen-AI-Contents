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