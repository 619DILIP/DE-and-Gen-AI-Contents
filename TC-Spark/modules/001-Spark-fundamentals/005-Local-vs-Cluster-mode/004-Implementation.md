## Local Mode Example

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("LocalModeExample").master("local[*]").getOrCreate()

spark.range(10).show()

spark.stop()
```

Run:

python script_name.py

------------------------------------------------------------------------

## Cluster Mode Example

spark-submit\
--master spark://cluster-master:7077\
--deploy-mode cluster\
script_name.py

------------------------------------------------------------------------

## Client Mode Example

spark-submit\
--master spark://cluster-master:7077\
--deploy-mode client\
script_name.py

------------------------------------------------------------------------

## Spark UI

Local Mode: http://localhost:4040

Cluster Mode: Access via cluster manager dashboard.