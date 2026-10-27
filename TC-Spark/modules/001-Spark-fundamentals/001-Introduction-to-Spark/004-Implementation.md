### Installing PySpark

``` bash
pip install pyspark
```

------------------------------------------------------------------------

### Creating a Spark Session

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder     .appName("SparkIntroduction")     .getOrCreate()
```

------------------------------------------------------------------------

### Creating a DataFrame

``` python
data = [
    ("Daniel", 95),
    ("Akshat", 96),
    ("Andrew", 90)
]

columns = ["Name", "Marks"]

df = spark.createDataFrame(data, columns)
df.show()
```

------------------------------------------------------------------------

### Filtering Data

``` python
df.filter(df.Marks > 90).show()
```

------------------------------------------------------------------------

### Aggregation Example

``` python
df.groupBy().avg("Marks").show()
```

------------------------------------------------------------------------

### Reading Data from CSV

``` python
df = spark.read.csv("data.csv", header=True, inferSchema=True)
df.printSchema()
df.show()
```

------------------------------------------------------------------------

### Writing Data

``` python
df.write.mode("overwrite").csv("output_folder")
```

------------------------------------------------------------------------

### Understanding Lazy Evaluation

Transformations such as:

-   filter()
-   select()
-   groupBy()

are not executed immediately. Spark executes them only when an action
like:

-   show()
-   collect()
-   count()

is triggered.