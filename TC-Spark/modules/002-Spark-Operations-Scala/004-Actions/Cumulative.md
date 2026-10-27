# Cumulative for the Actions
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites

- Knowledge of how to create an RDD in Spark.

## Objectives

- To learn about different action operations that can be applied to RDDs.

---

</details>
<details><summary>Description</summary>

## Description

- Actions are the operations that return a non-RDD value when applied to an RDD. The value of an action gets stored in the driver program. Examples of action operations are count(), collect(), first(), take(), etc.

## Actions in Spark-RDD

- To read an RDD result, use the `collect` operation on it. It will return all the data present inside the RDD.

- To get the total number of elements present in the RDD, use the `count` operation.

- The `reduce` operation gives the computed summarized result based on the function applied to the RDD.

- Use `first` if the goal is to get the first item from the RDD. `first` is an action.

- If the requirement is to get the first "n" items from the RDD, then use the `take` operation.

---

</details>

<details><summary>Implementation</summary> 

## Implementation

- For applying operations on an RDD, let's first create the RDD.

```
val data = Array(1, 2, 3, 3, 4, 5, 2)
val rdd1 = sc.parallelize(data)
``` 

- Use of `collect()`
```
rdd1.collect()
```
> Output: (1, 2, 3, 3, 4, 5, 2)

- Use of `count()` 
```
rdd1.count()
```
> This will return 7 as output.

- Use of `reduce()`
```
rdd1.reduce((x, y) => x + y)
```
> The output will be the sum of all the elements of the RDD. 

- Use of `first()`
```
rdd1.first()
```
> The output will be the first element of the RDD. 

- Use of `take()` 
```
rdd1.take(3)
```
> This will return the first 3 elements of the RDD. 

---

</details>
<details><summary>Summary</summary> 

## Summary

- Actions are the operations that bring laziness of transformations into action. Without applying any action function on a transformed RDD, it is not possible to generate a result.

- Examples of actions in Spark-RDD are collect(), count(), take(), reduce(), etc. 

---

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
