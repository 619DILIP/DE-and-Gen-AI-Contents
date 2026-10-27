## Description

- In this content we are going to see how to load/read a file stored in any location of any filesystem configured with Apache Spark and then how to store it back to filesystem. 

## Loading/Reading Data into RDD

- To load the data of a file into an Spark RDD, we can use two methods: 
  - `textFile()`
  - `wholeTextFiles()`

- **textFile():** This method is used to read the file as a collection of lines. It can read a single file, multiple files on the same folder, multiple files from different folders of any filesystem such as local filesystem, Hadoop's HDFS and Amazon S3. It has a optional parameter to include number of partitions against the default partitions created by spark based on the file size.

- Syntax:
```
SparkContext.textFile("path_of_the_file")
```

- **wholeTextFiles():** This method returns a pair-RDD that contains a filename and the content of the file in the form of tuple. 

- Syntax:
```
SparkContext.wholeTextFiles("path_of_the_file")
```

## Storing/Saving an RDD to FileSystem 

- After applying the transformation operations on your data you may want to store the final result back to the filesystem. To do so, we have one method as `saveAsTextFile()`, which helps in saving the data into one or many part files on the filesystem. 

- Syntax:
```
SparkContext.saveAsTextFile("FileSystem_path")
```

---

