<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

-   Understand what SparkSession is and why it is required.
-   Explain how SparkSession replaced older Spark entry points.
-   Create and configure a SparkSession using PySpark.
-   Use SparkSession to create DataFrames and execute SQL queries.
-   Work with Hive support and Spark catalog metadata.

</details>

<details><summary> Description </summary>

In Apache Spark 2.0 and later, SparkSession became the single unified
entry point to all Spark functionality.

Before Spark 2.0, developers had to work with multiple contexts:

-   SparkContext
-   SQLContext
-   HiveContext
-   StreamingContext

SparkSession simplifies this by:

-   Providing access to SparkContext
-   Replacing SQLContext and HiveContext
-   Supporting Structured Streaming
-   Enabling SQL, Hive, and DataFrame operations from a single object

In PySpark, a SparkSession object is typically referenced using the
variable name:

``` python
spark
```
### What is SparkSession?

SparkSession is the unified entry point to Spark functionality. It
allows you to:

-   Create DataFrames
-   Execute SQL queries
-   Access Spark configurations
-   Interact with Hive
-   Access metadata through the catalog
-   Access the underlying SparkContext

### Architecture Relationship

SparkSession\
↓\
SparkContext\
↓\
Cluster Manager (Standalone / YARN / Kubernetes)

SparkSession controls high-level operations, while SparkContext manages
cluster communication and resource allocation.

</details>

<details><summary>Real World Application</summary>

### Scenario: E-commerce Analytics

An e-commerce company processes daily transaction logs stored in
distributed storage and maintains product data in Hive.

Using SparkSession:

``` python
spark = SparkSession.builder     .appName("EcommerceAnalytics")     .enableHiveSupport()     .getOrCreate()

transactions = spark.read.csv("/data/transactions.csv", header=True)

transactions.createOrReplaceTempView("transactions")

daily_sales = spark.sql("""
    SELECT product_id, SUM(amount) as total_sales
    FROM transactions
    GROUP BY product_id
""")

daily_sales.write.mode("overwrite").saveAsTable("daily_sales_summary")
```

In this workflow, SparkSession acts as:

-   The entry point to distributed processing
-   The SQL execution engine
-   The bridge to Hive
-   The configuration controller

</details>

<details><summary> Implementation </summary>

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
```

</details>

<details><summary>Summary</summary>

-   SparkSession is the unified entry point to Apache Spark (introduced in Spark 2.0).
-   It replaces SQLContext and HiveContext.
-   It provides access to SparkContext.
-   It enables SQL, DataFrame, Hive, and Structured Streaming operations.
-   Multiple SparkSessions can exist but share the same SparkContext.
-   In PySpark, DataFrame is the primary abstraction.
-   SparkSession is required for all Spark-based data processing tasks.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
