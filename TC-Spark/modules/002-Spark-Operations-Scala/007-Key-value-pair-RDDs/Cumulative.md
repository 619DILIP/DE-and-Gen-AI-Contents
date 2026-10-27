# Cumulative for the Key Value Pair RDDs
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites

- Basic knowledge of creating RDDs in Spark

## Objectives

- To learn how to create pair-RDDs and what operations can be performed on them.

---

</details>
<details><summary>Description</summary>

## Description

- RDDs that hold elements in the form of key-value pairs are known as pair RDDs. Spark provides special operations on pair RDDs; for example, the `reduceByKey()` method can be used to aggregate data based on key.

- In this content, we will explore some transformations and actions that come in handy with key-value pair RDDs. 

## Transformations on Pair-RDD

- **groupByKey()** - It groups the values for each key.

- **reduceByKey()** - It is similar to the groupByKey operation, but it performs a map-side combine of values with the key.

- **aggregateByKey()** - It is similar to reduceByKey(), but the returned type can be different from the input type.

- **sortByKey()** - It sorts the dataset in ascending or descending order based on the key.

- **sampleByKey()** - It is used to get a subset of the RDD.

- **keys** - It is used to get the keys of an RDD.

- **values** - It is used to get the values of an RDD.

- **mapValues()** - It applies the map function on the values of the keys without changing the keys.

## Actions on Pair-RDD

- **collectAsMap()** - It collects the result as a map.

- **countByKey()** - It is used to get the count of elements for each key.  

- **lookup()** - It is used to get the values associated with the key by passing the key as a parameter.

- **reduceByKeyLocally()** - It merges the values for each key and returns the result immediately to the master. 

---

</details>



<details><summary>Implementation</summary> 

## Implementation

- Before applying any operations, let's first create a key-value pair RDD from an existing RDD using `map()`.
```
val rdd = sc.parallelize(List("hello", "hi", "is", "hi" , "hello", "hi", "am"))

val pairRDD = rdd.map(x => (x,1))

pairRDD.foreach(println)
```
- **Output:** 
```
("hello", 1)
("hi", 1)
("is", 1)
("hi", 1)
("hello", 1)
("hi", 1)
("am", 1)
```

- Applying the `reduceByKey()` operation on pairRDD. 
```
val rdd1 = pairRDD.reduceByKey((x,y) => x+y)
rdd1.foreach(println)
```
- **Output:**
```
("hello", 2)
("hi", 3)
("is", 1)
("am", 1)
```

- Applying the `groupByKey()` operation on pairRDD.
```
val rdd1 = pairRDD.groupByKey().map((x,y) => (x, sum(y)))
rdd1.foreach(println)
```
- The output will be the same as the reduceByKey() operation.


- Applying the `aggregateByKey()` operation on pairRDD.
```
val rdd1 = pairRDD.aggregateByKey(0)(_+_,_+_)
rdd1.foreach(println)
```
- The output will be the same as the reduceByKey() operation.


- Applying the `sortByKey()` operation on pairRDD.
```
val rdd1 = pairRDD.distinct().sortByKey()
rdd1.foreach(println)
```
- **Output:** 
```
("am", 1)
("hello", 1)
("hi", 1)
("is", 1)
```

- Applying `keys()` and `values()` operations
```
// Printing Keys
val rdd1 = pairRDD.keys()
rdd1.distinct().foreach(println)

// Printing Values
val rdd2 = pairRDD.reduceByKey((x,y) => x+y)
val rdd3 = rdd2.values()
rdd3.foreach(println)
```
- **Output keys**
```
hello
hi
is
am
```
- **Output Values**
```
2
3
1
1
```

- Applying the `collectAsMap()` operation on pairRDD.
```
pairRDD.collectAsMap().foreach(println)
```
- **Output:**
```
("hello", 1)
("hi", 1)
("is", 1)
("am", 1)
```

- Applying the `countByKey()` operation on pairRDD.
```
pairRDD.countByKey().foreach(println)
```
- **Output:**
```
("hello", 2)
("hi", 3)
("is", 1)
("am", 1)
```

---

</details>
<details><summary>Summary</summary> 

## Summary

- In Spark, there is a special type of RDD that holds key-value pairs, known as pair-RDD. Similar to regular RDDs, there are some transformation and action functions that can be applied to pair-RDDs. 

- Examples of transformation functions that can be applied to pair-RDDs are `reduceByKey()`, `combineByKey()`, `aggregateByKey()`, etc. 

- Examples of action functions that can be applied to pair-RDDs are `collectAsMap()`, `countByKey()`, `lookup()`, etc. 

---

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
