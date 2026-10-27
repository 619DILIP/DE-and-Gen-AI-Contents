# Cumulative for the Evolution of Hadoop topic

<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain how Hadoop evolved over time.
- Identify key milestones in Hadoop’s development.
- Understand the significance of major Hadoop releases.
- Recognize how Hadoop became an industry-standard Big Data framework.

</details>

<details><summary>Description</summary>

## Introduction

Hadoop did not appear overnight. It evolved from research projects and industry needs to handle massive web-scale data.

<br>

![Hadoop_Evolution](images/evolution.PNG)

<br>

---

## 2002 – The Beginning (Apache Nutch)

- Hadoop’s journey began with the **Apache Nutch** project.
- Doug Cutting and Mike Cafarella started Nutch to build a web search engine.
- Crawling and indexing billions of web pages required massive storage and processing.
- The cost of traditional infrastructure made this approach infeasible.
- A distributed, low-cost solution was needed.

---

## 2003 – Google File System (GFS)

- Google published a research paper on the **Google File System (GFS)**.
- The paper described how to store large datasets across distributed machines.
- This solved the storage problem for large-scale indexing.
- However, processing such massive data still required a solution.

---

## 2004 – MapReduce and NDFS

- Google released a paper on **MapReduce**, introducing a distributed processing model.
- Inspired by GFS, the Nutch team developed the **Nutch Distributed File System (NDFS)**.
- They later implemented MapReduce into Nutch.

This combination of distributed storage and distributed processing laid the foundation of Hadoop.

---

## 2006 – Birth of Hadoop

- The Apache community separated storage and processing components from Nutch.
- A new subproject called **Hadoop** was created.
- Hadoop was named after Doug Cutting’s son’s toy elephant.
- Doug Cutting joined Yahoo to scale Hadoop to thousands of nodes.

---

## 2007 – Large-Scale Adoption

- Yahoo deployed Hadoop on a 1,000-node cluster.
- Hadoop proved its ability to handle web-scale workloads.

---

## 2008 – Apache Top-Level Project

- Hadoop became an official Apache Top-Level Project.
- Companies like Facebook and The New York Times adopted Hadoop.
- Hadoop gained enterprise credibility.

---

## 2009 – Performance Milestone

- A Yahoo team used Hadoop to sort 1 terabyte of data in 62 seconds.
- This demonstrated Hadoop’s large-scale processing power.

---

## Major Hadoop Releases

### 2011–2012

- December 2011: Hadoop 1.0 released (included security and HBase support).
- March 2012: Version 1.0.1 bug-fix release.
- May 2012: Hadoop 2.0.0 alpha released (introduced YARN).
- October 2012: More stable Hadoop 2.x release with improved YARN.

YARN separated resource management from processing, making Hadoop more scalable.

---

### 2017–Present

- December 2017: Hadoop 3.0.0 released.
- 2018: Hadoop 3.0.1 and 3.1.0 introduced major bug fixes and improvements.
- Later 3.x releases improved stability, erasure coding, and performance.
- Hadoop 3.1.3 released in 2019.

Hadoop 3.x improved storage efficiency and cluster performance.

</details>

<details><summary>Real World Application</summary>

## Web-Scale Companies and Hadoop Evolution

The evolution of Hadoop directly influenced how large internet companies manage data today.

### 1. Yahoo

Yahoo was one of the first companies to adopt Hadoop at scale.

- Deployed Hadoop on 1,000-node clusters.
- Processed massive web indexing and search data.
- Demonstrated Hadoop’s ability to handle petabyte-scale workloads.

This large-scale deployment validated Hadoop’s reliability.

---

### 2. Facebook

Facebook adopted Hadoop to manage:

- User activity logs
- Messages
- Photos and videos
- Advertisement analytics

As user data grew exponentially, Hadoop’s distributed storage (HDFS) and parallel processing became essential.

---

### 3. Retail and E-Commerce

Retail companies use Hadoop to:

- Track customer purchases
- Generate product recommendations
- Analyze seasonal demand patterns
- Optimize supply chains

Example:
If a customer buys a smartphone, the system suggests accessories like a back cover or screen guard.

This recommendation engine is powered by large-scale data processing made possible by Hadoop’s evolution.

---

## Why Evolution Matters in Practice

- Hadoop 1.x allowed batch processing at scale.
- Hadoop 2.x (with YARN) enabled multiple frameworks like Spark.
- Hadoop 3.x improved storage efficiency and reduced infrastructure costs.

Without these evolutionary improvements, handling today’s social media, e-commerce, and smart city data would be extremely expensive and inefficient.

Hadoop’s evolution turned it from a research experiment into a backbone technology for modern data-driven enterprises.

</details>

<details><summary>Implementation</summary>

## How Hadoop Evolution Impacted Architecture

The evolution of Hadoop introduced key architectural improvements over time.

---

### Phase 1: Hadoop 1.x

- Included HDFS and MapReduce.
- MapReduce handled both processing and resource management.
- Suitable for batch processing workloads.
- Limited scalability for diverse workloads.

---

### Phase 2: Hadoop 2.x (Introduction of YARN)

- YARN separated resource management from MapReduce.
- Allowed multiple processing frameworks to run on Hadoop.
- Improved scalability and flexibility.
- Enabled support for tools like Spark.

---

### Phase 3: Hadoop 3.x

- Introduced erasure coding for better storage efficiency.
- Improved cluster performance.
- Enhanced fault tolerance.
- Reduced hardware costs.

---

## Key Evolutionary Improvements

Over time, Hadoop evolved to provide:

- Better resource management
- Improved scalability
- Increased storage efficiency
- Stronger fault tolerance
- Support for multiple processing engines

This evolution transformed Hadoop from a research project into a production-ready enterprise framework.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Hadoop originated from the Apache Nutch project.
- Google’s GFS and MapReduce papers inspired Hadoop’s development.
- Hadoop became an Apache Top-Level Project in 2008.
- Major releases (1.x, 2.x, 3.x) introduced important architectural improvements.
- The introduction of YARN significantly enhanced scalability.
- Hadoop evolved into a reliable, enterprise-grade Big Data platform.

<br>

![Hadoop_Evolution](images/evolution.PNG)

<br>

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
