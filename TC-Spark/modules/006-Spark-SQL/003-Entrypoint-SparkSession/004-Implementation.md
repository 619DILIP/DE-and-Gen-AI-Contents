### 1. Creating a SparkSession

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("SparkSessionExample").master("local[*]").getOrCreate()

print("Spark Version:", spark.version)
```

------------------------------------------------------------------------

### 2. Creating Multiple SparkSessions

``` python
new_session = spark.newSession()
print("New Session Created:", new_session)
```

Note: - Both sessions share the same SparkContext. - SQL configurations
and temporary views are session-specific.

------------------------------------------------------------------------

### 3. Setting and Retrieving Configurations

``` python
spark.conf.set("spark.sql.shuffle.partitions", "20")

configs = spark.conf.getAll()
print(configs)
```

------------------------------------------------------------------------

### 4. Creating a DataFrame

``` python
data = [("Python", 30000), ("Spark", 45000)]
df = spark.createDataFrame(data, ["Technology", "Salary"])
df.show()
```

------------------------------------------------------------------------

### 5. Running SQL Queries

``` python
df.createOrReplaceTempView("tech_table")

result = spark.sql("SELECT Technology, Salary FROM tech_table")
result.show()
```

------------------------------------------------------------------------

### 6. Enabling Hive Support

``` python
spark = SparkSession.builder.appName("HiveExample").enableHiveSupport() .getOrCreate()
```

``` python
df.write.mode("overwrite").saveAsTable("tech_hive_table")

hive_df = spark.sql("SELECT * FROM tech_hive_table")
hive_df.show()
```

------------------------------------------------------------------------

### 7. Accessing Catalog Metadata

``` python
spark.catalog.listDatabases().show()
spark.catalog.listTables().show()