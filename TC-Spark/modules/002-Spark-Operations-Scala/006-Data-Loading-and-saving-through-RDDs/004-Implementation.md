# Implementation

- For this implementation, we are using sc as SparkContext. 

- Reading a text file stored in local file system having path as "abc/xyz/demo.txt.
```
sc.textFile("/abc/xyz/demo.txt")
```

- Reading a text file with partition count.
```
sc.textFile("/abc/xyz/demo.txt", 4)
```

- Reading multiple files stored in same directory.
```
sc.textFile("/abc/xyz/demo.txt", "/abc/xyz/test.txt")
```

- Reading all files stored in same location.
```
sc.textFile("/abc/xyz/*")
```

- Reading multiple files stored in different location.
```
sc.textFile("/abc/pqr/test.txt", "/tvs/xyz/demo.txt")
```

- Reading file stored in HDFS.
```
sc.textFile("hdfs://abc/xyz/demo.txt")
```

- Reading file stored in Amazon S3. 
```
sc.textFile("s3a://abc/xyz/demo.txt")
```

- To get the filename along with its content use `wholeTextFiles()`.
```
sc.wholeTextFiles("/abc/xyz/demo.txt")
```

- To save the data of an RDD to the file in local filesystem use `saveAsTextFile()` method. Let's say we have an RDD named as "rdd1" which we have to store in the local filesystem under the "abc/xyz" directory.
```
rdd1.saveAsTextFile("/abc/xyz")
```

- To save the data of an RDD to HDFS location. 
```
rdd1.saveAsTextFile("hdfs://abc/xyz")
```

- To store the data of an RDD to Amazon S3 location.
```
rdd1.saveAsTextFile("s3a://abc/xyz") 
```

**Note**
> All these `saveAsTextFile` operations will create many partition files representing the RDD as part-00001, part-00002, etc. under the /abc/xyz directory, where each part file consists of some data of an RDD.

---

