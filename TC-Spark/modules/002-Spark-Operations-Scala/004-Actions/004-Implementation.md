## Implementation

- For applying some operations on RDD, let's first create the RDD.

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
> This will return 7 as an output.


- Use of `reduce()`
```
rdd1.reduce((x,y) => x+y)
```
> The output will be the sum of all the elements of RDD. 


- Use of `first()`
```
rdd1.first()
```
> The output will be the first element of an RDD. 


- Use of `take()` 
```
rdd1.take(3)
```
> This will return the first 3 elements of an RDD. 

---

