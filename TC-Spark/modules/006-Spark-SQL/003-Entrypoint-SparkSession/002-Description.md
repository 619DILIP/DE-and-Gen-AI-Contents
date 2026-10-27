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