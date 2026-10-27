## Implementation

- Before applying any operations let's first create a key-value pair RDD from an exisiting RDD using `map()`.
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

- Applying `reduceByKey()` operation on pairRDD. 
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

- Applying `groupByKey()` operation on pairRDD.
```
val rdd1 = pairRDD.groupByKey().map((x,y) => (x, sum(y)))
rdd1.foreach(println)
```
- Output will be same as reduceByKey() operation.


- Applying `aggregateByKey()` operation on pairRDD.
```
val rdd1 = pairRDD.aggregateByKey(0)(_+_,_+_)
rdd1.foreach(println)
```
- Output will be same as reduceByKey() operation.


- Applying `sortByKey()` operation on pairRDD.
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

- Applying `keys()` and `values()` operation
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

- Applying `collectAsMap()` operation on pairRDD.
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

- Applying `countByKey()` operation on pairRDD.
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

