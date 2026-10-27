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