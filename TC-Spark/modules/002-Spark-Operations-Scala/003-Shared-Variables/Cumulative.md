# Cumulative for the Shared Variables
<details><summary>Prerequisites and Learning Objectives</summary>

# Prerequisites
General experience using a computer.

# Learning Objectives
After completing this module, associates should be able to:

- Define the concept of Shared Variable
</details>
<details><summary>Description</summary>

# Introduction to Shared Variable 

- A shared variable is used to execute on a specific remote cluster node. Usually, it works on separate copies of all the variables that we use in functions. These specific variables are precisely copied to each machine.

- Shared variables are used to save the state, either at the module level or for the duration of a job. Using shared variables, we can share data across process instances associated with a module or a job. A process instance can read or update the data stored in a shared variable.

- Shared variables are the variables that are required to be used by many functions and methods in parallel.

- Types of Shared Variable 

    1.  Broadcast Variables
    2.  Accumulators
</details>


<details><summary>Implementation</summary> 

# Implementation 

1. Broadcast Variables in Spark

Broadcast variables are used to ship a copy of the variable with tasks.
We can create Spark broadcast variables from a variable `v`. For that, we need to call the `SparkContext.broadcast(v)` method. This variable is a wrapper around `v`. Also, by calling the `value` method we can access its value.

For example:

        scala> val broadcastVar1 = sc.broadcast(Array(10, 22, 53))
        broadcastVar1: org.apache.spark.broadcast.Broadcast[Array[Int]] = Broadcast(0)
        scala> broadcastVar1.value
        res0: Array[Int] = Array(10, 22, 53)

2. Accumulators

We can also create named or unnamed accumulators as a user. For example:

        scala> val accum1 = sc.longAccumulator("Accumulator1")
        accum1: org.apache.spark.util.LongAccumulator = LongAccumulator(id: 0, name: Some(Accumulator1), value: 0)
        scala> sc.parallelize(Array(10, 20, 30, 40)).foreach(x => accum1.add(x))
        ...
        10/26/22 13:32:06 INFO SparkContext: Tasks finished in 0.418104 s
        scala> accum1.value
        res2: Long = 10

</details>
<details><summary>Summary</summary> 

# Summary 

- A shared variable is used to execute on a specific remote cluster node. Usually, it works on separate copies of all the variables that we use in functions. These specific variables are precisely copied to each machine.

- Types of Shared Variable 

    1.  Broadcast Variables
    2.  Accumulators
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
