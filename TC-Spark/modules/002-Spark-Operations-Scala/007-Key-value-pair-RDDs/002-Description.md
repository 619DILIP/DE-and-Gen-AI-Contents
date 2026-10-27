## Description

- RDDs which holds element in the form of key-value pairs are known as pair RDDs. Spark provides special operations on pair RDDs such as `reduceByKey()` method can be used to aggregate data based on key. 

- In this content, we will be seeing some transformations and actions that comes handy with key-value pair RDDs. 

## Tranformations on Pair-RDD.

- **groupByKey()** - It groups the values of each key. 

- **reduceByKey()** - It is similar to groupByKey operation but it does the map-side combine of values with key. 

- **aggregateByKey()** - It is similar to reduceByKey() but the returned type can be different from the input type. 

- **sortByKey()** - It sorts the dataset in ascending or descending order based on the key.

- **sampleBykey()** - It is used to get the subset of the RDD.

- **keys** - It is used to get the keys of an RDD.

- **values** - It is used to get the values of an RDD.

- **mapValues()** - It applies the map function on the values of the keys without changing the keys.

## Actions on Pair-RDD

- **collectAsMap()** - It collects the result as a map.

- **countByKey()** - It is used to get the count of number of elements for each key.  

- **lookup()** - It is used to get the values associated with the key by passing key as a parameter to it. 

- **reduceByKeyLocally()** - It merge the values for each key and returns the result immediately to the master. 


---

