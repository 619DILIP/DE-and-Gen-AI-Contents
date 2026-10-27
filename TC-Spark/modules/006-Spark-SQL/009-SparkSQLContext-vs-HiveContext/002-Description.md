## Description

**SQLCONTEXT**

- The entry point into SparkSQL is SQLContext. Here's how you use the SparkContext to generate a SQLContext.

```scala
val sqlContext = new org.apache.spark.sql.SQLContext(sc)
```

-If you have the SQLContext you can strat work with DataFrame, DataSet etc.

**HIVE CONTEXT**

- The entry point into Hive is HiveContext. All of a SQLContext's features are available in a HiveContext. In fact, if you look at the documentation for the API, you can find that HiveContext extends SQLContext, which means it has support for the capabilities that SQLContext support and more (Hive specific functionalities)

```scala
public class HiveContext
extends SQLContext
implements Logging
```

- We can get a HiveContext using the SparkContext

```scala
val sqlContext = new org.apache.spark.sql.hive.HiveContext(sc)
```

| SQLCONTEXT                                                                                                                                                              | HIVE CONTEXT                                                                                                                                      |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| If we want to run the sql based queries on the dataframe instead of python or scala code use can use SQLcontext and write spark logic in sql creating temporary tables. | If we want to connect to hive and read data or write data to hive tables we can use HiveContext and perform the required operations on hive data. |
|val sparkConf = new SparkConf().setAppName("my app").setMaster("local[1]")                                                                                              | val sparkConf = new SparkConf().setAppName("my app").setMaster("local[1]")                                                                        |
| val sparkContext = new SparkContext(sparkConf)                                                                                                                          | val sparkContext = new SparkContext(sparkConf)                                                                                                    |
| val sql_context = SQLContext(sparkContext)                                                                                                                              | val hive_context = HiveContext(sparkContext)                                                                                                      |
|                                                                                                                                                                         |                                                                                                                                                   |

