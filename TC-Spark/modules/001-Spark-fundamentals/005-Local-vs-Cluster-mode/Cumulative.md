<details><summary> Learning Objectives </summary>

After completing this module, associates should be able to:

-   Differentiate between Local Mode and Cluster Mode
-   Understand where the Spark driver runs in each mode
-   Identify appropriate use cases for each mode
-   Execute applications in both modes
-   Understand how deployment mode affects performance and reliability
</details>

<details><summary> Description </summary>

## Local Mode

Local Mode runs Spark entirely on a single machine.

Characteristics:

-   Driver runs on the same machine as the application.
-   Executors run as threads within the same process.
-   No external cluster manager required.
-   Uses local CPU cores.

Master examples:

local\
local\[2\]\
local\[\*\]

Local mode is ideal for:

-   Learning
-   Development
-   Testing
-   Debugging small datasets

------------------------------------------------------------------------

## Cluster Mode

Cluster Mode runs Spark applications across multiple machines.

Characteristics:

-   Driver runs inside the cluster.
-   Executors run on worker nodes.
-   Resources managed by a cluster manager.
-   Client can disconnect after job submission.

Cluster managers include:

-   Standalone
-   YARN
-   Kubernetes

Cluster mode is used for:

-   Production workloads
-   Large-scale data processing
-   Fault-tolerant distributed execution

------------------------------------------------------------------------

## Client vs Cluster Deployment

Client Mode: - Driver runs on the submitting machine. - Executors run on
cluster nodes.

Cluster Mode: - Driver runs inside the cluster. - Job continues even if
client disconnects.

------------------------------------------------------------------------

## Key Differences

| Feature           | Local Mode               | Cluster Mode        |
|------------------|--------------------------|---------------------|
| Environment      | Single machine           | Multiple machines   |
| Driver Location  | Local machine            | Cluster node        |
| Executors        | Local threads            | Distributed nodes   |
| Scalability      | Limited                  | Highly scalable     |
| Use Case         | Development & Testing    | Production          |

</details>

<details><summary> Real World Application </summary>

### Development Workflow

1.  Develop and test Spark code locally.
2.  Validate using small datasets.
3.  Monitor using Spark UI.
4.  Deploy to cluster once validated.

------------------------------------------------------------------------

### Production Pipelines

Cluster mode is used in:

-   Fraud detection systems
-   Large-scale ETL jobs
-   Machine learning pipelines
-   Log processing systems

It enables:

-   Scalability
-   Fault tolerance
-   High availability

</details>

<details><summary> Implementation </summary>

## Local Mode Example

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder     .appName("LocalModeExample")     .master("local[*]")     .getOrCreate()

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

</details>

<details><summary> Summary </summary>

Local Mode: - Runs on single machine - Simple setup - Best for
development

Cluster Mode: - Runs across multiple machines - Scalable and fault
tolerant - Used in production

The same application code can run in both modes. Deployment mode
determines where the driver runs and how resources are managed.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>