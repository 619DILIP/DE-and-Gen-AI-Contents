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
