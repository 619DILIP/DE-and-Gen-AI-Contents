# Cumulative for the Working on DataSets
<details><summary>Prerequisites and Learning Objectives</summary>

# Prerequisites
General experience using a computer.

# Learning Objectives
Working principles of datasets.
</details>
<details><summary>Description</summary>

# Introduction to Data Set 

- It is a distributed collection of data. 
- It is a new interface added in Spark 1.6 that provides the benefits of RDDs.
- A Dataset can be constructed from JVM objects and then manipulated using functional transformations (map, flatMap, filter, etc.). 
- We can use the Dataset API in Scala, while Python does not support the Dataset API. 
- A Dataset is a strongly typed collection of domain-specific objects that can be transformed in parallel using functional or relational operations. Each Dataset also has an untyped view called a DataFrame, which is a Dataset of Rows.
</details>

<details><summary>Implementation</summary> 

# Implementation 

### Creating a Data Set

The most common way is by pointing Spark to some files on storage systems, using the read function available on a SparkSession.

        val people = spark.read.parquet("...").as[Person]

Datasets can also be created through transformations available on existing Datasets. For example, the following creates a new Dataset by applying a filter on the existing one:

        val names = people.map(_.name)  // in Scala; names is a Dataset[String]

</details>
<details><summary>Summary</summary> 

- A Dataset is a strongly typed collection of domain-specific objects that can be transformed in parallel using functional or relational operations. Each Dataset also has an untyped view called a DataFrame, which is a Dataset of Rows.
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
