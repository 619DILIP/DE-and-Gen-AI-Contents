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