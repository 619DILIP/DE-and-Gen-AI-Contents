## Description

- Transformation operations are used in manipulating RDD data and returns new RDD. 

- Transformations are evaluated lazily means they are not executed until an action is performed on it. 

## Transformations in Spark-RDD

- To get the unique elements from an RDD, use `distinct` operation.

- Use `filter` transformation for selecting elements based on condition. 

- To sort the data present inside the RDD in ascending or descending order, use `sortBy` operation. It will sort the data in ascending order when the condition is true and in descending order when the condition is false.

- `Map` transformation applies operation on each element present in RDD and returns a new RDD. The length of an old RDD and a new RDD both are the same.

- `flatMap` transformation is like `map`, but it also flattens the result after doing map operation. The length of the old RDD and new RDD may or may not be the same in flatMap case.

- If you have two RDDs and you need the combined data of both the RDDs into new RDD then use `union` operation.

- If you have two RDDs and you need the common data of both the RDDs into new RDD then use `intersection` operation.

- There are two operations through which you can increase or decrease the number of partitions for the RDD. 
  - Use `repartition` operation for increasing the number of partitions and `coalesce` for decreasing the number of partitions.

- Use `groupByKey()` to group each input key to an iterable value in the RDD. This will result in shuffling of data over the network.

- Similar to `groupByKey()` there is one more operation we can use on the Dataset that is `reduceByKey()`. Both do similar operation and result in same output, but the key difference between both is that reduceByKey() do the map side combine but groupBykey() doesn't.

---
