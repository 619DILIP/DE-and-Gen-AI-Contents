### Step 1: Create an RDD

``` python
data = [1, 2, 3, 3, 4, 5, 2]
rdd1 = sc.parallelize(data)
```

------------------------------------------------------------------------

### Using collect()

``` python
rdd1.collect()
```

Output: \[1, 2, 3, 3, 4, 5, 2\]

Returns all elements to the driver.

------------------------------------------------------------------------

### Using count()

``` python
rdd1.count()
```

Output: 7

Returns total number of elements in the RDD.

------------------------------------------------------------------------

### Using reduce()

``` python
rdd1.reduce(lambda x, y: x + y)
```

Output: 20

Aggregates elements using the provided function.

------------------------------------------------------------------------

### Using first()

``` python
rdd1.first()
```

Output: 1

Returns the first element of the RDD.

------------------------------------------------------------------------

### Using take(n)

``` python
rdd1.take(3)
```

Output: \[1, 2, 3\]

Returns the first n elements.