<details><summary> Learning Objectives </summary>

After completing this module, learners will be able to:

-   Install and configure PySpark using pip
-   Understand how Spark runs in local mode
-   Create and manage SparkSession
-   Configure Spark settings programmatically
-   Run Spark applications using Python scripts
-   Use Spark inside Jupyter Notebook
-   Access and understand Spark UI
-   Handle common configuration and memory issues

</details>

<details><summary> Description </summary>

Apache Spark can be used directly from Python using **PySpark**. For
development and learning purposes, Spark runs in **Local Mode**, which
means:

-   It runs entirely on your machine
-   Uses your CPU cores
-   Does not require a distributed cluster
-   Does not require Hadoop setup

When installed via pip, PySpark bundles the required Spark runtime,
making setup significantly easier than traditional JVM-based
installation.

</details>

<details><summary> Real World Application </summary>

Even though this setup runs locally, it mirrors how Spark behaves in
real production environments.

### 1. Data Engineering Teams

Data engineers develop Spark jobs locally using PySpark before deploying
them to:

-   YARN clusters
-   Kubernetes clusters
-   Cloud-based Spark services (Databricks, EMR, Synapse)

Local setup ensures:

-   Faster development cycles
-   Easier debugging
-   Testing before production deployment

------------------------------------------------------------------------

### 2. Data Science & Machine Learning

Data scientists:

-   Prototype ML pipelines locally
-   Perform feature engineering
-   Test distributed transformations
-   Validate datasets

Once validated locally, the same PySpark code can scale to process
terabytes of data in production.

------------------------------------------------------------------------

### 3. Real-Time Analytics Systems

Companies developing:

-   Fraud detection systems
-   Recommendation engines
-   Log analytics pipelines
-   IoT data processing

Often build and test Structured Streaming jobs locally before pushing to
distributed clusters.

------------------------------------------------------------------------

### 4. Enterprise Workflow Development

Organizations follow this workflow:

1.  Develop Spark job locally (using pip-based PySpark)
2.  Test using sample datasets
3.  Monitor performance via Spark UI
4.  Deploy to cluster using spark-submit

This local setup is the first step in that pipeline.

</details>

<details><summary> Implementation </summary>

## Step 1: Install PySpark

Install using pip:

``` bash
pip install pyspark
```

Verify installation:

``` bash
python -c "import pyspark; print(pyspark.__version__)"
```

If a version number prints successfully, installation is complete.

------------------------------------------------------------------------

## Step 2: Understanding Local Mode

When you use:

``` python
.master("local[*]")
```

It means:

-   local → run on your local machine

-   -   → use all available CPU cores

You can also specify:

``` python
.master("local[2]")
```

This will use only 2 CPU cores.

------------------------------------------------------------------------

## Step 3: Creating a SparkSession

Create a file named spark_setup_test.py:

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder     .appName("SparkSetupTest")     .master("local[*]")     .getOrCreate()

print("Spark Version:", spark.version)

spark.stop()
```

Run:

``` bash
python spark_setup_test.py
```

If it runs without errors, Spark is correctly configured.

------------------------------------------------------------------------

## Step 4: Basic DataFrame Example

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder     .appName("DataFrameExample")     .master("local[*]")     .getOrCreate()

data = [
    ("Alice", 25),
    ("Bob", 30),
    ("Charlie", 35)
]

columns = ["Name", "Age"]

df = spark.createDataFrame(data, columns)

df.show()
df.printSchema()

spark.stop()
```

------------------------------------------------------------------------

## Step 5: Configuring Spark Programmatically

You can configure Spark settings inside your application:

``` python
spark = SparkSession.builder     .appName("ConfigExample")     .master("local[*]")     .config("spark.driver.memory", "2g")     .config("spark.executor.memory", "2g")     .config("spark.sql.shuffle.partitions", "4")     .getOrCreate()
```

Common configurations:

-   spark.driver.memory → Memory for driver
-   spark.executor.memory → Memory for executor
-   spark.sql.shuffle.partitions → Controls shuffle partitions
-   spark.app.name → Application name

------------------------------------------------------------------------

## Step 6: Running Spark in Jupyter Notebook

Install Jupyter:

``` bash
pip install notebook
```

Start Notebook:

``` bash
jupyter notebook
```

Inside notebook:

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder     .master("local[*]")     .appName("NotebookExample")     .getOrCreate()

spark.range(10).show()
```

Notebook-based development is ideal for:

-   Data exploration
-   Teaching
-   Interactive analytics

------------------------------------------------------------------------

## Step 7: Accessing Spark UI

When running any Spark job, open:

http://localhost:4040

Spark UI provides:

-   Job execution timeline
-   Stage breakdown
-   Task distribution
-   Memory usage
-   Shuffle details

If port 4040 is busy, Spark automatically tries 4041, 4042, etc.

------------------------------------------------------------------------

## Step 8: Project Structure Recommendation

For better organization:

    spark_project/
    │
    ├── data/
    ├── scripts/
    │   ├── spark_app.py
    │   └── utils.py
    ├── notebooks/
    │   └── analysis.ipynb
    └── requirements.txt

requirements.txt:

    pyspark

------------------------------------------------------------------------

## Step 9: Common Errors and Fixes

### 1. Java not found

Even in Python setup, Java must exist in system.

Check:

``` bash
java -version
```

Install Java if missing.

------------------------------------------------------------------------

### 2. Memory Error

Reduce memory usage:

``` python
.config("spark.driver.memory", "1g")
```

------------------------------------------------------------------------

### 3. Slow Performance

Limit shuffle partitions:

``` python
.config("spark.sql.shuffle.partitions", "4")
```

------------------------------------------------------------------------

### 4. Multiple Spark Sessions Error

Always stop session:

``` python
spark.stop()
```

------------------------------------------------------------------------

## Step 10: Running Spark as a Standalone Python Application

Use spark-submit (optional advanced step):

``` bash
spark-submit spark_setup_test.py
```

This simulates how Spark jobs run in production environments.

</details>

<details><summary> Summary </summary>

In this module, we learned:

-   How to install PySpark using pip
-   How Spark runs in local mode
-   How to create and configure SparkSession
-   How to work with DataFrames
-   How to configure memory and partitions
-   How to use Spark in Jupyter Notebook
-   How to monitor jobs using Spark UI
-   How to troubleshoot common issues

For distributed cluster deployment, Spark can later be integrated with
YARN or Kubernetes, but for learning and development, this Python-only
setup is fully sufficient.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>