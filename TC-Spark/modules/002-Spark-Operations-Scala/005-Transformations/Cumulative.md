# Cumulative for the Transformations
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites

- Knowledge of how to create an RDD in Spark.

## Objectives

- To learn about different transformation operations that can be applied to RDDs.

---

</details>
<details><summary>Description</summary>

## Description

- Transformation operations are used to manipulate RDD data and return a new RDD.

- Transformations are evaluated lazily, meaning they are not executed until an action is performed on them.

## Transformations in Spark-RDD

- To get the unique elements from an RDD, use the `distinct` operation.

- Use the `filter` transformation to select elements based on a condition.

- To sort the data present inside the RDD in ascending or descending order, use the `sortBy` operation. It will sort the data in ascending order when the condition is true and in descending order when the condition is false.

- The `map` transformation applies an operation to each element present in the RDD and returns a new RDD. The length of the old RDD and the new RDD is the same.

- The `flatMap` transformation is like `map`, but it also flattens the result after the map operation. The length of the old RDD and the new RDD may or may not be the same in the case of `flatMap`.

- If you have two RDDs and need the combined data of both RDDs into a new RDD, use the `union` operation.

- If you have two RDDs and need the common data of both RDDs in a new RDD, use the `intersection` operation.

- There are two operations through which you can increase or decrease the number of partitions for the RDD. 
  - Use the `repartition` operation to increase the number of partitions and `coalesce` to decrease the number of partitions.

- Use `groupByKey()` to group each input key into an iterable value in the RDD. This will result in the shuffling of data over the network.

- Similar to `groupByKey()`, there is one more operation we can use on the Dataset, which is `reduceByKey()`. Both perform similar operations and result in the same output, but the key difference is that `reduceByKey()` performs a map-side combine while `groupByKey()` does not.

---
</details>

<details><summary>Implementation</summary> 

## Implementation

- For applying some operations on an RDD, let's first create the RDD.

```
val data = Array(1, 2, 3, 3, 4, 5, 2)
val rdd1 = sc.parallelize(data)
``` 

- Using `distinct()` to get unique elements.
```
rdd1.distinct().collect()
```

- Using `filter` to get elements that are less than 3.
```
val filter_rdd = rdd1.filter(x => x < 3)
filter_rdd.collect()
```
 
- `sortByKey()` example 
```
rdd1.sortBy(x => x, true).collect()
rdd1.sortBy(x => x, false).collect()
```

- Using `map()` to split the list of items. 
```
val rdd1 = sc.parallelize(Array("hello my friend", "how are you"))

rdd1.map(_.split(" ")).collect()
```
- This will result in:
> Array(Array("hello", "my", "friend"), Array("how", "are", "you"))

- Using `flatMap()` to split the list of items.
```
val rdd1 = sc.parallelize(Array("hello my friend", "how are you"))

rdd1.flatMap(_.split(" ")).collect()
```
- This will result in:
> Array("hello", "my", "friend", "how", "are", "you")

- Applying `union()` on RDDs.  
```
val rdd1 = sc.parallelize(Array(1, 2, 3))
val rdd2 = sc.parallelize(Array(4, 5, 6))

rdd1.union(rdd2).collect()
```
- Output will be:
> Array(1, 2, 3, 4, 5, 6)

- Applying `intersection()` on RDDs.
```
val rdd1 = sc.parallelize(Array(1, 2, 3, 5))
val rdd2 = sc.parallelize(Array(4, 5, 2))

rdd1.intersection(rdd2).collect()
```
- Output will be:
> Array(2, 5)

- Example of `coalesce` and `repartition`. 
```
val rdd1 = sc.parallelize(Array(10, 20, 30, 20, 40))
val rdd2 = rdd1.repartition(5)
val rdd3 = rdd2.coalesce(2)
```

**Note:**
> `repartition` can be used for increasing or decreasing the number of partitions, but it is recommended to use `coalesce` when the need is to decrease the partitions as it doesn't result in shuffling all the data over the network.

- Example of `groupByKey()`

```
val rdd1 = sc.parallelize(Array("A", "B", "B", "D", "A"))
val rdd2 = rdd1.map(char => (char, 1))
val rdd3 = rdd2.groupByKey().map((a, b) => (a, sum(b)))
```

- Example of `reduceByKey()`.
```
val rdd1 = sc.parallelize(Array("A", "B", "B", "D", "A"))
val rdd2 = rdd1.map(char => (char, 1))
val rdd3 = rdd2.reduceByKey((a, b) => (a + b))
```
**Note:**
> - `groupByKey()` and `reduceByKey()` both come under wide transformations, meaning they both result in the shuffling of data between partitions.
> - To choose between both depends on the size and type of data. Use `reduceByKey()` over `groupByKey()` as it performs a map-side combine and hence sends less data to reduce over the network, making it preferable if we apply some aggregate functions like sum or average on the dataset. 
> - Opt for `groupByKey()` when there is no need for a map-side combine or when the data size is small. 

---

</details>
<details><summary>Summary</summary> 

## Summary 

- Transformation operations are used to manipulate data present inside an RDD, and they return a new RDD. They are evaluated lazily, meaning they are not executed until an action is performed on them. 

- Examples of Transformations in Spark-RDD include `filter()`, `map()`, `flatMap()`, `reduceByKey()`, etc.

---
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
