<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

-   Start and verify HDFS services.
-   Execute basic HDFS file system commands.
-   Manage files and directories in HDFS.
-   Understand practical use cases of common HDFS commands.

</details>
<details><summary>Description</summary>

## Starting Hadoop Services

Before executing any HDFS commands, ensure that the Hadoop Distributed
File System (HDFS) services are running.

    start-dfs.sh

This starts:

-   NameNode
-   Secondary NameNode
-   DataNodes

To verify services:

    jps


## Accessing HDFS

You can interact with HDFS using:

    hdfs dfs

or

    hadoop fs

------------------------------------------------------------------------
## Common HDFS Commands

| Command            | Description                                   |
|--------------------|-----------------------------------------------|
| `-ls`              | List files and directories                   |
| `-mkdir`           | Create a directory                           |
| `-rm -r`           | Remove file or directory recursively         |
| `-rmdir`           | Delete an empty directory                    |
| `-put`             | Upload file from local system to HDFS       |
| `-get`             | Download file from HDFS to local system     |
| `-cat`             | Display file content                         |
| `-du`              | Show file or directory size                  |
| `-count`           | Count directories, files, and total size     |
| `-mv`              | Move file or directory                       |
| `-cp`              | Copy file or directory                       |
| `-setrep`          | Change replication factor                    |
| `-tail`            | Display last part of file                    |
| `-df`              | Show HDFS filesystem space usage             |
| `-touchz`          | Create an empty file                         |
| `-appendToFile`    | Append content to an existing file           |
| `-checksum`        | Display file checksum                        |
| `-find`            | Search for files in HDFS                     |


</details>

<details><summary>Real World Application</summary>

## Real-World Usage in Enterprise Hadoop Clusters

In production environments, HDFS commands are used daily by data engineers, DevOps teams, and platform administrators to manage large-scale distributed data systems.

### 1️⃣ Data Ingestion Pipelines

- Raw datasets from applications, IoT devices, logs, and databases are uploaded using:

        hdfs dfs -put

- In automated workflows, ingestion scripts push hourly/daily batch files into structured directories such as:

        /data/raw/2025/02/11/

- Engineers often validate successful uploads using:

        hdfs dfs -ls
        hdfs dfs -du -h

This ensures that the expected files are present and match the expected size.

---

### 2️⃣ Data Lake Organization

Enterprise data lakes follow strict directory hierarchies:

    /data/raw
    /data/processed
    /data/curated
    /archive

Teams create structured folders using:

        hdfs dfs -mkdir -p

This ensures proper separation between:
- Raw ingested data
- Transformed data
- Production-ready datasets

---

### 3️⃣ Monitoring and Log Analysis

Application logs are continuously written to HDFS.

Engineers monitor logs in real-time using:

        hdfs dfs -tail

This is especially useful when:
- Debugging Spark jobs
- Investigating failed MapReduce tasks
- Monitoring streaming jobs

---

### 4️⃣ Storage Optimization and Capacity Planning

Administrators regularly check:

        hdfs dfs -df -h
        hdfs dfs -du -h

This helps them:
- Monitor cluster storage usage
- Prevent disk overflows
- Plan for capacity expansion

---

### 5️⃣ Replication and Data Reliability

Critical datasets such as financial transactions or customer data require higher durability.

Replication factor is adjusted using:

        hdfs dfs -setrep 3 /path/file

Increasing replication:
- Improves fault tolerance
- Ensures availability during node failures

---

### 6️⃣ Cleanup and Lifecycle Management

Temporary and intermediate files are removed using:

        hdfs dfs -rm -r

Organizations often implement:
- Scheduled cleanup jobs
- Archiving policies
- Automated retention scripts

This prevents storage bloat and maintains cluster performance.

---

In short, these commands are not just academic — they are the operational toolkit that keeps Hadoop ecosystems stable, efficient, and production-ready.

</details>


<details><summary>Implementation</summary>

## Step-by-Step Practical Implementation

Below is a structured workflow that simulates a real-world HDFS operation scenario.

---

### ✅ Step 1: Verify Hadoop Services

Start HDFS:

    start-dfs.sh

Verify services:

    jps

Ensure:
- NameNode is running
- DataNode(s) are running

---

### ✅ Step 2: Explore Root Directory

List root contents:

    hdfs dfs -ls /

Check available space:

    hdfs dfs -df -h /

This confirms cluster health and storage availability.

---

### ✅ Step 3: Create Structured Data Directory

Create main directory:

    hdfs dfs -mkdir /data

Create nested structure:

    hdfs dfs -mkdir -p /data/raw/2025/02/11
    hdfs dfs -mkdir -p /data/processed

Verify:

    hdfs dfs -ls /data

---

### ✅ Step 4: Upload a File to HDFS

Upload local file:

    hdfs dfs -put /local/path/file.txt /data/raw/2025/02/11/

Confirm upload:

    hdfs dfs -ls /data/raw/2025/02/11/

Check file size:

    hdfs dfs -du -h /data/raw/2025/02/11/

---

### ✅ Step 5: View and Inspect File Content

Display entire file:

    hdfs dfs -cat /data/raw/2025/02/11/file.txt

View last few lines:

    hdfs dfs -tail /data/raw/2025/02/11/file.txt

Generate checksum:

    hdfs dfs -checksum /data/raw/2025/02/11/file.txt

---

### ✅ Step 6: Copy and Move Files

Copy file to processed folder:

    hdfs dfs -cp /data/raw/2025/02/11/file.txt /data/processed/

Move file:

    hdfs dfs -mv /data/raw/2025/02/11/file.txt /archive/

---

### ✅ Step 7: Change Replication Factor

Increase replication to 3:

    hdfs dfs -setrep 3 /data/processed/file.txt

Verify replication:

    hdfs dfs -ls /data/processed/

---

### ✅ Step 8: Download File to Local System

    hdfs dfs -get /data/processed/file.txt /local/path/

---

### ✅ Step 9: Remove Files or Directories

Delete file:

    hdfs dfs -rm /data/processed/file.txt

Delete directory recursively:

    hdfs dfs -rm -r /data/raw

Delete empty directory:

    hdfs dfs -rmdir /archive

---

### 🔎 Optional Advanced Operations

Search files:

    hdfs dfs -find /data -name "*.txt"

Create empty file:

    hdfs dfs -touchz /data/marker.txt

Append content:

    hdfs dfs -appendToFile localfile.txt /data/marker.txt

Count files and directories:

    hdfs dfs -count /data

---

This workflow reflects how data engineers manage ingestion, validation, organization, monitoring, replication, and cleanup within a production Hadoop environment.

</details>

<details><summary>Summary</summary>

## Module Recap

In this module, we moved beyond basic command memorization and explored how HDFS is actually operated in real-world environments.

We covered:

- Starting and verifying HDFS services using `start-dfs.sh` and `jps`.
- Accessing the distributed file system using `hdfs dfs` and `hadoop fs`.
- Core file system operations such as:
  - Listing directories (`-ls`)
  - Creating structured folders (`-mkdir -p`)
  - Uploading and downloading files (`-put`, `-get`)
  - Viewing file content (`-cat`, `-tail`)
  - Managing storage (`-du`, `-df`)
  - Copying and moving data (`-cp`, `-mv`)
  - Cleaning up data (`-rm -r`, `-rmdir`)
- Adjusting replication for fault tolerance using `-setrep`.
- Validating file integrity using `-checksum`.
- Searching and counting files using `-find` and `-count`.

We also simulated a practical workflow that mirrors enterprise usage, including:

- Data ingestion into structured directories
- Validation and inspection of uploaded data
- Replication management for reliability
- Storage monitoring and capacity awareness
- Cleanup and lifecycle management

By the end of this module, you should be able to:

- Confidently navigate HDFS.
- Manage distributed files and directories.
- Perform operational checks in a Hadoop cluster.
- Understand how these commands support production data engineering workflows.

These commands form the operational foundation of Hadoop environments. Mastery here enables you to work effectively with large-scale distributed storage systems.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>