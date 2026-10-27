## Description

- Actions are the operations that return a non-RDD value when applied on RDD. The value of action gets stored in the driver program. Example of action operations are count(), collect(), first(), take(), etc.

## Actions in Spark-RDD

- To read a RDD result use `collect` operation on it. It will return all the data present inside RDD.

- To get the total number of elements present in the RDD, use `count` operation.

- `reduce` operation gives the computed summarized result based on function applied on RDD. 

- Use `first` if the need is to get the first item from RDD. `first` is an action. 

- If the requirement is to get the first "n" items from RDD, then use `take` operation.

---

