## Summary

- In the above module we have learned the RDD (Resilient Distributed Dataset) is the basic form of data abstraction in Apache Spark and Spark Core. It is a fundamental Spark data structure. As fault-tolerant, immutable distributed groups of objects, RDDs cannot be altered after they have been created. Logical partitions are created for each dataset in RDD so that they can be calculated on several cluster nodes.

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

