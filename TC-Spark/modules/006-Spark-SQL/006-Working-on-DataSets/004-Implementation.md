# Implementation 

### Creating a Data Set

The most common way is by pointing Spark to some files on storage systems, using the read function available on a SparkSession.


        val people = spark.read.parquet("...").as[Person]


Datasets can also be created through transformations available on existing Datasets. For example, the following creates a new Dataset by applying a filter on the existing one:


        val names = people.map(_.name)  // in Scala; names is a Dataset[String]

