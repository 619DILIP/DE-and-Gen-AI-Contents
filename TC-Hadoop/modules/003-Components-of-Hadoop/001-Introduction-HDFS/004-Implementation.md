## How HDFS Works in Practice

Let’s understand how HDFS operates step by step.

---

### Step 1: File Upload to HDFS

When a client uploads a file:

- The file is split into large blocks.
- Each block is assigned to different DataNodes.
- Replicas of each block are created.

---

### Step 2: Metadata Management

The NameNode:

- Records file name
- Stores block IDs
- Tracks block locations
- Maintains permissions

Metadata is stored in memory for fast access.

---

### Step 3: Read Operation

When a client reads a file:

- The client contacts the NameNode for block locations.
- The NameNode provides DataNode details.
- The client directly reads data from DataNodes.

The NameNode is not involved in actual data transfer.

---

### Step 4: Fault Tolerance Handling

If a DataNode fails:

- Heartbeat signals stop.
- NameNode marks it as dead.
- Missing blocks are replicated from healthy nodes.

The system continues functioning without data loss.

---

## Why HDFS is Suitable for Big Data

- Handles very large files efficiently.
- Designed for high-throughput batch processing.
- Runs on commodity hardware.
- Provides automatic fault recovery.