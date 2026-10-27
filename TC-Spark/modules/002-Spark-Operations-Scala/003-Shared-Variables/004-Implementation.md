# Implementation 

1. Broadcast Variables in Spark

Broadcast Variables despite shipping a copy of it with tasks.
We can create Spark broadcast variables from a variable v. For that, we need to call SparkContext.broadcast(v) method. This variable is a wrapper around v. Also, by calling the value method we can access its value.

For Example:

        scala> val broadcastVar1 = sc.broadcast(Array(10, 22, 53))
        broadcastVar1: org.apache.spark.broadcast.Broadcast[Array[Int]] = Broadcast(0)
        scala> broadcastVar1.value
        res0: Array[Int] = Array(10, 22, 53)

2. Accumulators

We can also create named or unnamed accumulators, as a user. 
For Example:


        scala> val accum1 = sc.longAccumulator("Accumulator1")
        accum1: org.apache.spark.util.LongAccumulator = LongAccumulator(id: 0, name: Some(Accumulator1), value: 0)
        scala> sc.parallelize(Array(10, 20, 30, 40)).foreach(x => accum.add(x))
        ...
        10/26/22 13:32:06 INFO SparkContext: Tasks finished in 0.418104 s
        scala> accum1.value
        res2: Long = 10

