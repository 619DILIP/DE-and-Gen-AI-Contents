# Cumulative for the SparkSQLContext vs HiveContext
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites

- Basic knowledge of the Hadoop file system, Python or Scala, or Java programming language, and the basics of any distributed database.

## Learning Objectives

- After completing this module, anyone will be able to understand the difference between SparkSqlContext and HiveContext.

</details>
<details><summary>Description</summary>

## Description

**SQLCONTEXT**

- The entry point into SparkSQL is SQLContext. Here's how you use the SparkContext to generate a SQLContext.

```scala
val sqlContext = new org.apache.spark.sql.SQLContext(sc)
```

- If you have the SQLContext, you can start working with DataFrame, DataSet, etc.

**HIVE CONTEXT**

- The entry point into Hive is HiveContext. All of SQLContext's features are available in HiveContext. In fact, if you look at the documentation for the API, you can find that HiveContext extends SQLContext, which means it has support for the capabilities that SQLContext supports and more (Hive-specific functionalities).

```scala
public class HiveContext
extends SQLContext
implements Logging
```

- We can get a HiveContext using the SparkContext.

```scala
val hiveContext = new org.apache.spark.sql.hive.HiveContext(sc)
```

| SQLCONTEXT                                                                                                                                                              | HIVE CONTEXT                                                                                                                                      |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| If we want to run SQL-based queries on the DataFrame instead of Python or Scala code, we can use SQLContext and write Spark logic in SQL, creating temporary tables. | If we want to connect to Hive and read data or write data to Hive tables, we can use HiveContext and perform the required operations on Hive data. |
| val sparkConf = new SparkConf().setAppName("my app").setMaster("local[1]")                                                                                              | val sparkConf = new SparkConf().setAppName("my app").setMaster("local[1]")                                                                        |
| val sparkContext = new SparkContext(sparkConf)                                                                                                                          | val sparkContext = new SparkContext(sparkConf)                                                                                                    |
| val sqlContext = SQLContext(sparkContext)                                                                                                                              | val hiveContext = HiveContext(sparkContext)                                                                                                      |
|                                                                                                                                                                         |                                                                                                                                                   |

</details>

<details><summary>Summary</summary> 

## Summary

- In the above module, we have learned that the entry point into SparkSQL is SQLContext. Here's how you use the SparkContext to generate a SQLContext.

```scala
val sqlContext = new org.apache.spark.sql.SQLContext(sc)
```

- If you have the SQLContext, you can start working with DataFrame, DataSet, etc.

**HIVE CONTEXT**

- The entry point into Hive is HiveContext. All of SQLContext's features are available in HiveContext. In fact, if you look at the documentation for the API, you can find that HiveContext extends SQLContext, which means it has support for the capabilities that SQLContext supports and more (Hive-specific functionalities).

```scala
public class HiveContext
extends SQLContext
implements Logging
```

- We can get a HiveContext using the SparkContext.

```scala
val hiveContext = new org.apache.spark.sql.hive.HiveContext(sc)
```
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
