## Implementation

**RDD Creation**

- RDDs are typically created in one of two ways: by parallelizing an existing collection or by referencing a dataset in an external storage system (HDFS, S3, and many more).

```scala
val spark:SparkSession = SparkSession.builder()
      .master("local[1]")
      .appName("SparkByExamples.com")
      .getOrCreate()    
```

</br>

![RDD](Images/rdd.PNG)

</br>

**sparkContext.parallelize()**

- The `sparkContext.parallelize() ` method is used to parallelize an existing collection in your driver program and this method is used to create RDD.

```scala
val dataSeq = Seq(("Java", 20000), ("Python", 100000), ("Scala", 3000))   
val rdd=spark.sparkContext.parallelize(dataSeq)
```

**sparkContext.textFile()**

- Using `textfile()` function or method we can read a text file into RDD.

```scala
val rdd2 = spark.sparkContext.textFile("/path/textFile.txt")
```

**sparkContext.wholeTextFiles()**

- `sparkContext.wholeTextFiles()` function returns a PairRDD with the key being the file path and value being file content.
  
```scala
val rdd3 = spark.sparkContext.wholeTextFiles("/path/textFile.txt")
```

**sparkContext.emptyRDD()**

- Using `sparkContext.emptyRDD()` method on SparkContext we can create an RDD with no data and this method is used to create an empty RDD with no partition.

```scala
val rdd = spark.sparkContext.emptyRDD 
val rddString = spark.sparkContext.emptyRDD[String] 
```

**Creating empty RDD with partition**

- An empty RDD may sometimes need to be written to files using partitioning; in this case, you should create an empty RDD with partition.

```scala
val rdd2 = spark.sparkContext.parallelize(Seq.empty[String])
```

**RDD Parallelize and repartition**

- When we use parallelize(), textFile(), or wholeTextFiles() methods to launch RDD, the data is automatically partitioned based on resource availability.

**getNumPartitions** - Returns a number of the partitions our dataset was divided into. Any transformations that are applied to an RDD execute concurrently. For each partition of the cluster, Spark will execute a single task.

```scala
println("initial partition count:"+rdd.getNumPartitions)
```

**Set parallelize manually** - The second parameter of these operations, such as `sparkContext.parallelize(dataSeq, 10) `, can be used to explicitly set the number of partitions if needed.

**Repalallize using repartition and coalesce** - Spark offers two methods for repartitioning RDDs: the `repartition()` method, also known as full shuffle, which shuffles data from all nodes, and the `coalesce()` method, which shuffles data from the minimum number of nodes. For example, if your data is divided into four partitions, coalesce(2) will only move data from two nodes.

```scala
val reparRdd = rdd.repartition(4)
println("re-partition count:"+reparRdd.getNumPartitions)
```

- `repartition()` or `coalesce()` methods also returns a new RDD.
