# Cumulative for the Data Loading and Saving through RDDs
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites 

- Knowledge of different filesystems.

## Objectives

- To learn how to read/load data from the filesystem to RDD. 
- To learn how to store the result of the RDD back to the filesystem.

---
</details>
<details><summary>Description</summary>

## Description

- In this content, we are going to see how to load/read a file stored in any location of any filesystem configured with Apache Spark and then how to store it back to the filesystem. 

## Loading/Reading Data into RDD

- To load the data of a file into a Spark RDD, we can use two methods: 
  - `textFile()`
  - `wholeTextFiles()`

- **textFile():** This method is used to read the file as a collection of lines. It can read a single file, multiple files in the same folder, or multiple files from different folders of any filesystem such as the local filesystem, Hadoop's HDFS, and Amazon S3. It has an optional parameter to include the number of partitions against the default partitions created by Spark based on the file size.

- Syntax:
```
SparkContext.textFile("path_of_the_file")
```

- **wholeTextFiles():** This method returns a pair RDD that contains a filename and the content of the file in the form of a tuple. 

- Syntax:
```
SparkContext.wholeTextFiles("path_of_the_file")
```

## Storing/Saving an RDD to FileSystem 

- After applying transformation operations on your data, you may want to store the final result back to the filesystem. To do so, we have one method: `saveAsTextFile()`, which helps in saving the data into one or many part files on the filesystem. 

- Syntax:
```
SparkContext.saveAsTextFile("FileSystem_path")
```

---

</details>


<details><summary>Implementation</summary> 

# Implementation

- For this implementation, we are using `sc` as SparkContext. 

- Reading a text file stored in the local filesystem with the path "abc/xyz/demo.txt":
```
sc.textFile("/abc/xyz/demo.txt")
```

- Reading a text file with a specified partition count:
```
sc.textFile("/abc/xyz/demo.txt", 4)
```

- Reading multiple files stored in the same directory:
```
sc.textFile("/abc/xyz/demo.txt", "/abc/xyz/test.txt")
```

- Reading all files stored in the same location:
```
sc.textFile("/abc/xyz/*")
```

- Reading multiple files stored in different locations:
```
sc.textFile("/abc/pqr/test.txt", "/tvs/xyz/demo.txt")
```

- Reading a file stored in HDFS:
```
sc.textFile("hdfs://abc/xyz/demo.txt")
```

- Reading a file stored in Amazon S3: 
```
sc.textFile("s3a://abc/xyz/demo.txt")
```

- To get the filename along with its content, use `wholeTextFiles()`:
```
sc.wholeTextFiles("/abc/xyz/demo.txt")
```

- To save the data of an RDD to a file in the local filesystem, use the `saveAsTextFile()` method. Let's say we have an RDD named "rdd1" that we have to store in the local filesystem under the "abc/xyz" directory:
```
rdd1.saveAsTextFile("/abc/xyz")
```

- To save the data of an RDD to an HDFS location: 
```
rdd1.saveAsTextFile("hdfs://abc/xyz")
```

- To store the data of an RDD to an Amazon S3 location:
```
rdd1.saveAsTextFile("s3a://abc/xyz") 
```

**Note**
> All these `saveAsTextFile` operations will create multiple partition files representing the RDD as part-00001, part-00002, etc. under the /abc/xyz directory, where each part file consists of some data of an RDD.

---

</details>
<details><summary>Summary</summary> 

## Summary

- Spark allows loading data from filesystems such as local, HDFS, and S3 to an RDD. RDD provides two methods for reading from the filesystem: `textFile()` and `wholeTextFiles()`. 

- To load the data present in files stored in HDFS or S3, we must use `hdfs://` and `s3a://` as prefixes to the file path.

- To store the result of an RDD back to any filesystem after applying transformations on it, use the `saveAsTextFile()` method. 

---

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
