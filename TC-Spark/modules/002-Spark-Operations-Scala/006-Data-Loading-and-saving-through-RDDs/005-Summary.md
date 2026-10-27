## Summary

- Spark allows to load data from filesystems such as local, HDFS and S3 to an RDD. RDD provides two methods using which we can read from filesystem, one is `textFile()` and another one is `wholeTextFiles()`. 

- To load the data present in files stored in HDFS or S3, we must use the hdfs:// and s3a:// as prefix to the file path.

- To store the result of RDD back to any file system, after applying transformations on it, use `saveAsTextFile()` method. 

---

