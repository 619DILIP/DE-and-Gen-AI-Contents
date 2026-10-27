<details><summary> Learning Overview </summary>

After Completing This Module, Learners Will Be Able To:

-   Explain how variables behave in distributed Spark applications
-   Define Shared Variables and their purpose
-   Differentiate between Broadcast Variables and Accumulators
-   Understand performance implications of shared variables
-   Implement Broadcast Variables in PySpark
-   Implement Accumulators in PySpark
-   Avoid common mistakes when using shared variables

</details>

<details><summary> Description </summary>

## Variable Behavior in Distributed Systems

In Spark, code runs in two components:

-   Driver Program
-   Executors (Worker Nodes)

When a variable is defined in the driver:

``` python
x = 10
```

And used inside a transformation:

``` python
rdd.map(lambda v: v + x)
```

Spark serializes the function and sends a copy of `x` to each executor.

Important points:

-   Executors do not share memory.
-   Each task works on its own copy.
-   Changes inside executors do not reflect back to the driver automatically.

This creates challenges when:

-   Large lookup data must be reused.
-   Global counters must be updated.
-   State must be tracked across tasks.

To address these issues, Spark provides Shared Variables.

## Types of Shared Variables

Spark provides two types:

1.  Broadcast Variables (Read-only shared data)
2.  Accumulators (Aggregated updates from workers)

Shared Variables improve performance, reduce network overhead, and
enable safe distributed state management.

</details>

<details><summary> Real World Application </summary>

## Broadcast Variable Example

You have millions of transaction records and a small lookup dictionary
containing country codes.

Instead of sending the dictionary repeatedly to every task, you
broadcast it once to all executors.

Common uses:

-   Lookup tables
-   Configuration settings
-   Static reference data
-   Model parameters

## Accumulator Example

You are processing log files and need to count how many records contain
errors.

Each executor processes part of the data and increments an accumulator.
The driver retrieves the final aggregated count.

Common uses:

-   Counting invalid records
-   Monitoring job metrics
-   Debugging distributed tasks
-   Tracking statistics

</details>

<details><summary> Implementation </summary>

## Broadcast Variables

Broadcast variables distribute read-only data to executors efficiently.

### Creating a Broadcast Variable

``` python
from pyspark import SparkContext

sc = SparkContext("local", "BroadcastApp")

lookup_data = {
    1: "India",
    2: "USA",
    3: "Germany"
}

broadcast_lookup = sc.broadcast(lookup_data)
```

### Using Broadcast Variable

``` python
rdd = sc.parallelize([1, 2, 3, 1, 2])

result = rdd.map(lambda x: broadcast_lookup.value[x])
print(result.collect())
```

Key Points:

-   Sent once per executor
-   Read-only
-   Reduces network traffic

## Accumulators

Accumulators allow executors to update a shared value safely.

### Creating an Accumulator

``` python
from pyspark import SparkContext

sc = SparkContext("local", "AccumulatorApp")

error_count = sc.accumulator(0)
```

### Using Accumulator

``` python
def check_error(record):
    global error_count
    if "ERROR" in record:
        error_count += 1

logs = sc.parallelize([
    "INFO Start",
    "ERROR Failure",
    "INFO Continue",
    "ERROR Crash"
])

logs.foreach(check_error)

print("Total errors:", error_count.value)
```

Key Points:

-   Workers update value
-   Driver reads final value
-   Useful for counters and monitoring

</details>

<details><summary> Summary </summary>

-   Shared Variables solve distributed memory isolation challenges.
-   Broadcast Variables share read-only data efficiently across executors.
-   Accumulators aggregate updates from executors back to the driver.
-   Proper use improves performance and scalability.
-   Understanding Shared Variables is essential for production-grade Spark applications.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>

