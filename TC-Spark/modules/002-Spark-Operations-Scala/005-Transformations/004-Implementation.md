## Implementation

- For applying some operations on RDD, let's first create the RDD.

```
val data = Array(1, 2, 3, 3, 4, 5, 2)
val rdd1 = sc.parallelize(data)
``` 


- Using `distinct()` to get unique elements.
```
rdd1.distinct().collect()
```

- Using `filter` to get elements which are less than 3.
```
val filter_rdd = rdd1.filter(x => x<3)
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

rdd1.flatMap(_.split(" ")).collect 
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
val rdd1 = sc.parallelize(Array(10, 20 , 30 , 20 , 40))
val rdd2 = rdd1.repartition(5)
val rdd3 = rdd2.coalesce(2)
```

**Note:**
> `repartition` can be used for increasing or decreasing the number of partitions but, it is recommended to use `coalesce` when the need is to decrease the partitions as it doesn't result in shuffling of all the data over the network.


- Example of `groupByKey()`

```
val rdd1 = sc.parallelize(Array("A", "B", "B", "D", "A"))
val rdd2 = rdd1.map(char => (char, 1))
val rdd3 = rdd2.groupByKey().map((a,b) => (a, sum(b)))
```

- Example of `reduceByKey()`.
```
val rdd1 = sc.parallelize(Array("A", "B", "B", "D", "A"))
val rdd2 = rdd1.map(char => (char, 1))
val rdd3 = rdd2.reduceByKey((a,b) => (a + b))
```
**Note:**
> - `groupByKey()` and `reduceByKey()` both come under wide transformation that means they both result in shuffling of data between partitions.
> - To choose between both depends on the size and type of data. Use `reduceByKey()` over `groupByKey()` as it does the map side combine and hence sends less amount of data to reduce over the network and preferable if we apply some aggregate functions like sum, average on the dataset. 
> - Go for `groupByKey()` when there is no need of map side combine or when the data is less in size. 

---

