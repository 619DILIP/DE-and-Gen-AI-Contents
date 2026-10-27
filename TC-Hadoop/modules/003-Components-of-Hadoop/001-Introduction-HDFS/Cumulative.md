<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what Hadoop is.
- Describe HDFS and its purpose.
- Identify key HDFS components.
- Understand how HDFS ensures fault tolerance.
- Explain the role of NameNode, DataNode, and Secondary NameNode.

</details>

<details><summary>Description</summary>

## What is Hadoop?

Apache Hadoop is an open-source framework designed for:

- Distributed storage
- Distributed processing

It allows large datasets to be stored and processed across clusters of commodity hardware.

Hadoop uses the MapReduce programming model for data processing and HDFS for distributed storage.

---

## Core Hadoop Components

Hadoop consists of three major components:

- HDFS (Hadoop Distributed File System)
- YARN (Resource Management)
- MapReduce (Processing Framework)

This module focuses on HDFS.

---

## What is a Distributed File System?

When a dataset becomes too large for a single machine, it must be divided and stored across multiple machines.

A distributed file system:

- Stores data across several machines.
- Allows users to access data as if it were stored in one location.
- Provides scalability and reliability.

---

## Hadoop Distributed File System (HDFS)

HDFS is designed to store very large files across multiple machines in a cluster.

### Key Features of HDFS

- Distributed storage
- High fault tolerance
- High throughput
- Scalability

HDFS splits large files into blocks (default size: 128 MB or 256 MB) and distributes them across multiple nodes.

---

## HDFS Architecture

An HDFS cluster typically consists of:

- One NameNode (Master)
- Multiple DataNodes (Workers)
- Secondary NameNode (Checkpoint Node)

![DataNode](Images/DataNode.PNG)

---

### 1. NameNode (Master Node)

The NameNode:

- Manages the file system namespace.
- Maintains metadata (file names, permissions, block locations).
- Keeps track of which DataNode stores which block.
- Records changes to the file system.

It does not store actual data blocks.

---

### 2. DataNode (Worker Nodes)

DataNodes:

- Store actual data blocks.
- Handle read and write requests from clients.
- Send heartbeat signals to the NameNode every few seconds.

If a DataNode fails to send heartbeats for a certain time, the NameNode marks it as dead and re-replicates the data blocks to maintain fault tolerance.

---

### 3. Secondary NameNode

The Secondary NameNode:

- Periodically merges the FSImage and Edit logs.
- Creates checkpoints.
- Prevents the Edit log from growing indefinitely.

It is not a backup NameNode but a checkpointing node.

---

## HDFS Data Replication

To ensure reliability:

- Each data block is replicated (default replication factor = 3).
- Copies are stored on different DataNodes.
- If one node fails, data remains accessible.

This replication mechanism makes HDFS fault tolerant.

</details>

<details><summary>Real World Application</summary>

## Large-Scale Data Storage in Social Media

Companies such as Facebook use HDFS to store:

- User posts
- Images and videos
- Activity logs
- Interaction data

Since billions of users generate data daily, traditional storage systems are insufficient.

HDFS allows:

- Storage of petabytes of data
- Reliable access despite hardware failures
- Scalable infrastructure by simply adding more machines

This makes HDFS ideal for high-volume environments like social media platforms and large e-commerce systems.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Hadoop is a distributed framework for storing and processing large datasets.
- HDFS is Hadoop’s storage layer.
- HDFS follows a master-worker architecture.
- NameNode manages metadata.
- DataNodes store actual data blocks.
- Secondary NameNode performs checkpointing.
- Data replication ensures fault tolerance.

HDFS enables scalable, reliable, and distributed storage for Big Data environments.

![Architecture](Images/hdfs.PNG)

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
