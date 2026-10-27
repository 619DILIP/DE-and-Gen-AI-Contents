<details>
<summary>Learning Objectives</summary>

After completing this module, associates should be able to:

- Explain why YARN was introduced in Hadoop 2.0.
- Describe how YARN separates resource management from data processing.
- Identify and explain the responsibilities of each YARN component.
- Illustrate the lifecycle of an application running on YARN.
- Compare YARN-enabled processing with traditional MapReduce-only architecture.
- List practical enterprise use cases of YARN.

</details>

<details>
<summary>Description</summary>

# Introduction to YARN

YARN (Yet Another Resource Negotiator) is Hadoop’s cluster resource management layer. It was introduced in Hadoop 2.0 to address scalability and flexibility limitations in the original Hadoop 1.x architecture.

In Hadoop 1.x:
- MapReduce handled both **data processing** and **resource management**.
- The JobTracker was responsible for everything.
- This created scalability bottlenecks and limited support to only MapReduce.

YARN solves this by separating concerns:
- **Resource management**
- **Application processing**

This architectural separation allows multiple distributed processing engines (not just MapReduce) to run on the same Hadoop cluster.

![Example](Images/YARN.PNG)

In simple terms:

YARN is the traffic controller of the Hadoop cluster.  
It decides who gets CPU, who gets memory, and where tasks should run.

---

## Why YARN Was Introduced

YARN was introduced to:

1. Remove the single JobTracker bottleneck.
2. Improve scalability for large clusters.
3. Allow multiple data processing frameworks.
4. Increase cluster utilization.
5. Enable multi-tenant environments.

Without YARN, Hadoop would remain limited to MapReduce workloads.

---

## Core Responsibilities of YARN

YARN is responsible for:

- Managing cluster-wide resources (CPU, memory).
- Scheduling applications.
- Allocating containers to applications.
- Monitoring node health.
- Restarting failed tasks.
- Supporting multiple processing frameworks.

It does NOT process data itself.  
It manages the environment where processing happens.

---

## Features of YARN

1. **Scalability**  
   Can manage clusters with thousands of nodes efficiently.

2. **Compatibility**  
   Supports MapReduce, Spark, Tez, Flink, and other distributed frameworks.

3. **Improved Cluster Utilization**  
   Dynamically allocates resources instead of reserving them statically.

4. **Multi-tenancy**  
   Multiple users and departments can share the same cluster.

5. **Resource Sharing**  
   Applications compete fairly using scheduling policies.

6. **Fault Tolerance**  
   Detects node failures and reassigns tasks automatically.

---

# Architecture of YARN

YARN consists of three major components:

- ResourceManager
- NodeManager
- ApplicationMaster

![YARN Architecture](Images/YARN_ARC.PNG)

---

## 1. ResourceManager

The ResourceManager (RM) is the master authority of the cluster.

It has two main parts:

### a) Scheduler
- Allocates resources to applications.
- Uses scheduling policies like FIFO, Capacity Scheduler, or Fair Scheduler.
- Makes decisions based on resource availability.

### b) ApplicationManager
- Accepts job submissions.
- Launches the ApplicationMaster.
- Restarts ApplicationMaster if it fails.

There is typically only one ResourceManager per cluster.

---

## 2. NodeManager

The NodeManager (NM) runs on every node in the cluster.

Responsibilities:
- Monitors resource usage (CPU, memory, disk, network).
- Manages containers.
- Reports health status to the ResourceManager.
- Kills containers that exceed resource limits.

Each machine in the cluster runs exactly one NodeManager.

---

## 3. ApplicationMaster

Every application submitted to YARN gets its own ApplicationMaster.

Responsibilities:
- Negotiates resources from ResourceManager.
- Requests containers.
- Launches tasks on NodeManagers.
- Tracks task progress.
- Handles failures.
- Reports completion status.

If the ApplicationMaster fails, the ResourceManager can restart it.

---

# Understanding Containers in YARN

A container is a logical bundle of resources:

- Memory
- CPU
- Network

When an application needs resources:
1. ApplicationMaster requests containers.
2. ResourceManager allocates containers.
3. NodeManager launches tasks inside containers.

Containers isolate applications and ensure fair resource usage.

---

# Lifecycle of a YARN Application

1. Client submits application to ResourceManager.
2. ResourceManager launches an ApplicationMaster container.
3. ApplicationMaster registers with ResourceManager.
4. ApplicationMaster requests required containers.
5. ResourceManager allocates containers.
6. NodeManagers launch tasks inside containers.
7. ApplicationMaster monitors execution.
8. Application completes and resources are released.

---

# Advantages of YARN Over Hadoop 1.x

| Hadoop 1.x | Hadoop 2.x (YARN) |
|------------|-------------------|
| Single JobTracker | Separate ResourceManager & ApplicationMaster |
| Only MapReduce | Multiple frameworks supported |
| Scalability limitations | Highly scalable |
| Limited resource sharing | Efficient dynamic allocation |

---
</details>

<details>
<summary>Real World Application</summary>

YARN is widely used in enterprise big data environments where multiple workloads need to share the same cluster efficiently.

It acts as the backbone resource manager for several popular distributed frameworks.

---

## 1. Batch Processing

Organizations use YARN to run large-scale ETL (Extract, Transform, Load) jobs.

Examples:
- Data warehouse batch updates
- Daily report generation
- Financial transaction processing

Frameworks used:
- MapReduce
- Apache Spark
- Apache Hive

---

## 2. Streaming Processing

YARN supports real-time and near real-time data processing.

Examples:
- Fraud detection systems
- Log monitoring
- Real-time recommendation engines

Frameworks used:
- Apache Spark Streaming
- Apache Flink
- Apache Storm

---

## 3. Interactive SQL Processing

Business analysts use interactive query engines running on YARN.

Examples:
- Ad-hoc queries on massive datasets
- Dashboard analytics
- Business intelligence reporting

Frameworks used:
- Apache Hive
- Apache Impala (in some setups)
- Presto (in YARN-integrated environments)

---

## 4. Machine Learning Workloads

YARN enables distributed ML model training.

Examples:
- Customer churn prediction
- Image classification pipelines
- Recommendation system training

Frameworks used:
- Spark MLlib
- TensorFlow on YARN

---

## 5. Multi-Tenant Enterprise Environments

Large companies allow multiple departments to share a single cluster:

- Data Engineering team runs ETL jobs.
- Data Science team runs ML training.
- Business Intelligence team runs SQL queries.

YARN ensures fair scheduling and resource isolation among all users.

---

# Companies Using YARN

Many large organizations use Hadoop clusters managed by YARN, including:

- Financial institutions
- E-commerce platforms
- Telecom companies
- Social media platforms
- Government data systems

YARN enables them to process petabytes of data efficiently.

</details>

<details>
<summary>Implementation</summary>

YARN is implemented as part of Hadoop 2.x and above. It runs as a distributed service within a Hadoop cluster.

---

## 1. Cluster Setup

A typical YARN cluster includes:

- One ResourceManager (master node)
- Multiple NodeManagers (worker nodes)

Each worker node contributes CPU and memory resources to the cluster.

---

## 2. Configuration Files

YARN is configured using:

- yarn-site.xml
- core-site.xml
- hdfs-site.xml
- mapred-site.xml

Key configurations include:
- ResourceManager hostname
- Memory allocation limits
- CPU core allocation
- Scheduler type (FIFO, Capacity, Fair)

---

## 3. Starting YARN Services

After configuration, YARN services are started using:

start-yarn.sh

This launches:
- ResourceManager
- NodeManagers

Administrators can verify running services using:
jps command

---

## 4. Submitting an Application to YARN

When a user submits a job:

Example:
hadoop jar example.jar

Process flow:
1. Client submits job to ResourceManager.
2. ResourceManager launches ApplicationMaster.
3. ApplicationMaster negotiates containers.
4. Tasks run inside containers on NodeManagers.
5. Results are returned to the client.

---

## 5. Monitoring YARN

YARN provides a web UI for monitoring.

Default:
http://<ResourceManagerHost>:8088

From the UI, administrators can:
- View running applications
- Check resource usage
- Monitor node health
- Kill applications if necessary

---

## 6. Scheduling Policies

Administrators can configure:

- FIFO Scheduler (First In First Out)
- Capacity Scheduler (Queues with guaranteed capacity)
- Fair Scheduler (Resources distributed fairly)

Choice depends on organizational requirements.

---

## 7. High Availability (HA)

In production environments:

- Multiple ResourceManagers can be configured.
- Active/Standby setup ensures fault tolerance.
- ZooKeeper is often used for coordination.

---

# Practical Deployment Scenario

Example:

An e-commerce company:

- Stores logs in HDFS.
- Runs Spark jobs for recommendation systems.
- Executes Hive queries for sales reports.
- Trains ML models weekly.

All these workloads share the same cluster.

YARN dynamically allocates resources so no team blocks another.

</details>


<details>
<summary>Summary</summary>

In this module, we learned:

- YARN is Hadoop’s resource management layer.
- It separates resource management from data processing.
- Core components:
  - ResourceManager
  - NodeManager
  - ApplicationMaster
- It enables multiple distributed frameworks to run on the same cluster.
- It improves scalability, flexibility, and efficiency.

</details>

<details>
<summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
