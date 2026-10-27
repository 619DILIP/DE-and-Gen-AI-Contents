# Cumulative for the Basic RDD Operations
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites

- Knowledge about how to create an RDD in Spark.

## Objectives

- To learn about different operations that can be applied to RDDs.

---
</details>
<details><summary>Description</summary>

## Description

- Two types of operations can be applied to RDDs: 
  - Transformation
  - Action 

## Transformation 

- Transformation operations are used to manipulate RDD data and return a new RDD. 

- Transformations are evaluated lazily, meaning they are not executed until an action is performed on them. 

- Each transformation is logically connected with its parent RDD through a lineage graph. 

- Transformations are of two types:
  - Narrow Transformation
  - Wide Transformation

**1. Narrow Transformation** 

- In a narrow transformation, there is no data movement between RDD partitions after an operation is applied to it. Examples of narrow transformations include map(), flatMap(), filter(), union(), mapPartitions(), etc.

**2. Wide Transformation**

- A wide transformation results in the movement of data between RDD partitions after an operation is applied to it. Shuffling of data occurs in wide transformations. Examples of wide transformations include groupByKey(), reduceByKey(), aggregateByKey(), join(), repartition(), etc. 

## Action

- Actions are the operations that return a non-RDD value when applied to an RDD. The value from an action is stored in the driver program. Examples of action operations include count(), collect(), first(), take(), etc.

---

</details>
<details><summary>Real World Application</summary>

</details>
<details><summary>Implementation</summary> 

> For Basic RDD operations implementation, refer to the `Action` and `Transformation` modules.
</details>
<details><summary>Summary</summary> 

## Summary

- Operations on RDDs are of two types: Transformation and Action. Transformations are operations used to manipulate the dataset, and their return type is always an RDD. Action operations, on the other hand, are used to compute all the RDDs at once after applying all the transformations. Their return type is always a non-RDD value. 

- Transformations can be categorized as narrow and wide transformations. Narrow transformations do not result in shuffling of data, whereas wide transformations always result in shuffling of data over the network.

- Some examples of transformations are map(), filter(), groupByKey(), and repartition(). Some examples of actions are reduce(), collect(), take(), and first(). 

---
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
