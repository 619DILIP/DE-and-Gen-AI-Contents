## Description

- Two types of operations can be applied on RDDs: 
  - Transformation
  - Action 

## Transformation 

- Transformation operations are used in manipulating RDD data and returns new RDD. 

- Transformations are evaluated lazily means they are not executed until an action is performed on it. 

- Each transformation is connected logically with its parent RDD through lineage graph. 

- Transformations are of two types:
  - Narrow Transformation
  - Wide Transformation

**1. Narrow Transformation** 

- In narrow transformation, there is no data movement between RDD's partitions after an operation is applied on it. Examples of narrow transformations are map(), flatMap(), filter(), union(), mapPartition(), etc.


**2. Wide Transformation**

- Wide transformation results in movement of data between RDD's partitions after an operation is applied on it. Shuffling of data happens in wide transformation. Examples of wide transformations are groupByKey(), reduceByKey(), aggregateByKey(), join(), repartition(), etc. 


## Action

- Actions are the operations that return a non-RDD value when applied on RDD. The value of action gets stored in the driver program. Example of action operations are count(), collect(), first(), take(), etc.

---

