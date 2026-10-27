## Summary

- In the above module we have learned the entry point into SparkSQL is SQLContext. Here's how you use the SparkContext to generate a SQLContext.

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
