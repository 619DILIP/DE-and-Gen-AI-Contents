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