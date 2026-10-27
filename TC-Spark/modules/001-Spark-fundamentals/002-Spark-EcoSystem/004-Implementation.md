Below is a simple end-to-end ecosystem example:

``` python
from pyspark.sql import SparkSession
from pyspark.ml.feature import VectorAssembler
from pyspark.ml.clustering import KMeans

spark = SparkSession.builder.appName("SparkEcosystemDemo").getOrCreate()

# Load data
df = spark.read.csv("data.csv", header=True, inferSchema=True)

# SQL query
df.createOrReplaceTempView("data_table")
spark.sql("SELECT * FROM data_table LIMIT 5").show()

# ML example
assembler = VectorAssembler(inputCols=["feature1", "feature2"], outputCol="features")
data = assembler.transform(df)

kmeans = KMeans(k=2, seed=1)
model = kmeans.fit(data)

# Show cluster centers
print(model.clusterCenters())
```

This demonstrates integration of Spark SQL and MLlib within one unified
engine.