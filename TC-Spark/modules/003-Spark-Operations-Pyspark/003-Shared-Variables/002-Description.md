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