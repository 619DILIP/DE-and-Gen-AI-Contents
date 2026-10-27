<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

-   Define what Actions are in Spark.
-   Differentiate between Transformations and Actions.
-   Explain how Actions trigger execution in Spark.
-   Apply commonly used RDD action operations.
-   Understand performance implications of certain actions like `collect()`.


</details>

<details><summary>Description</summary>

In Apache Spark, RDD operations are categorized into two main types:

-   Transformations
-   Actions

Transformations are lazy. They define a logical execution plan but do
not immediately execute.

Actions trigger execution.

Without an Action, Spark will not execute the transformations applied to
an RDD.

Actions return non-RDD values and send the final result to the driver
program.

This execution model allows Spark to optimize the computation using DAG
scheduling before running the job.

### What Are Actions?

Actions are operations that:

-   Trigger computation of the RDD lineage.
-   Execute the Directed Acyclic Graph (DAG).
-   Return results to the driver.
-   Save results to external storage if required.

When an Action is called, Spark:

1.  Builds the execution plan.
2.  Optimizes it.
3.  Distributes tasks across executors.
4.  Collects the final result.

------------------------------------------------------------------------

### Common RDD Actions

| Action           | Description                                      |
|------------------|--------------------------------------------------|
| collect()        | Returns all elements of the RDD to the driver    |
| count()          | Returns the total number of elements             |
| reduce()         | Aggregates elements using a specified function   |
| first()          | Returns the first element                        |
| take(n)          | Returns the first n elements                     |
| foreach()        | Applies a function to each element               |
| saveAsTextFile() | Saves the RDD data to storage                    |

------------------------------------------------------------------------

### Important Considerations

-   `collect()` brings all data to the driver. Avoid using it for large datasets.
-   `reduce()` requires a commutative and associative function.
-   Actions cause actual cluster computation.
-   Without an Action, transformations remain unevaluated.


</details>

<details><summary>Real World Application</summary>

### Scenario: Server Log Analysis

An organization processes large volumes of server logs stored in
distributed storage.

Engineers may need to:

-   Count total log entries.
-   Retrieve a sample record for validation.
-   Aggregate error counts.
-   Save processed logs back to storage.

Example:

``` python
logs = sc.textFile("/data/server_logs.txt")

# Total log count
total_logs = logs.count()

# First log entry
first_log = logs.first()

# Count error logs
error_count = logs.filter(lambda x: "ERROR" in x).count()
```

In this scenario:

-   `count()` measures system activity.
-   `first()` validates log structure.
-   `filter().count()` helps detect system issues.
-   `collect()` is used carefully for small debugging samples.

Actions make distributed computations visible and usable at the driver
level.


</details>

<details><summary>Implementation</summary>

### Step 1: Create an RDD

``` python
data = [1, 2, 3, 3, 4, 5, 2]
rdd1 = sc.parallelize(data)
```

------------------------------------------------------------------------

### Using collect()

``` python
rdd1.collect()
```

Output: \[1, 2, 3, 3, 4, 5, 2\]

Returns all elements to the driver.

------------------------------------------------------------------------

### Using count()

``` python
rdd1.count()
```

Output: 7

Returns total number of elements in the RDD.

------------------------------------------------------------------------

### Using reduce()

``` python
rdd1.reduce(lambda x, y: x + y)
```

Output: 20

Aggregates elements using the provided function.

------------------------------------------------------------------------

### Using first()

``` python
rdd1.first()
```

Output: 1

Returns the first element of the RDD.

------------------------------------------------------------------------

### Using take(n)

``` python
rdd1.take(3)
```

Output: \[1, 2, 3\]

Returns the first n elements.


</details>

<details><summary>Summary</summary>

## Summary

-   Actions trigger execution in Spark.
-   They return non-RDD values to the driver.
-   Transformations remain lazy until an Action is applied.
-   Common actions include `collect()`, `count()`, `reduce()`, `first()`, and `take()`.
-   Care must be taken when using `collect()` on large datasets.
-   Actions are essential for producing results in Spark applications.


</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>

