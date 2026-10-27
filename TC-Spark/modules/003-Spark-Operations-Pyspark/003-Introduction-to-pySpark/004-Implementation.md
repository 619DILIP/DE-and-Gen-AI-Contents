## Step 1: Import Required Libraries

``` python
import pyspark
from pyspark.sql import SparkSession
import pandas as pd
```

------------------------------------------------------------------------

## Step 2: Create a Spark Session

The SparkSession is the entry point for working with DataFrames and SQL
in Spark.

``` python
spark = SparkSession.builder.appName("Spark-Introduction").getOrCreate()
```

Explanation:

-   appName() sets the application name
-   getOrCreate() creates a new Spark session or retrieves an existing
    one

------------------------------------------------------------------------

## Step 3: Loading Dataset into PySpark

To load a dataset into Spark, use the read method.

``` python
df_pyspark = spark.read.csv("Example.csv", header=True, inferSchema=True)
df_pyspark.show()
```

Explanation:

-   header=True treats the first row as column names
-   inferSchema=True automatically detects data types
-   show() displays the data

------------------------------------------------------------------------

## Inspecting Data

``` python
df_pyspark.printSchema()
df_pyspark.columns
df_pyspark.describe().show()
```

These methods help understand the structure and statistics of the
dataset.