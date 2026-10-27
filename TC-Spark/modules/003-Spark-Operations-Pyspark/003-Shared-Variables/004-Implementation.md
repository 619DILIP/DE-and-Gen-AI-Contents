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