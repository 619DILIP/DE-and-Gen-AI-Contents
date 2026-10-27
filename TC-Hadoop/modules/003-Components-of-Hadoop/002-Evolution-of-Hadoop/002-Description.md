## Introduction

Hadoop did not appear overnight. It evolved from research projects and industry needs to handle massive web-scale data.

<br>

![Hadoop_Evolution](Images/evolution.PNG)

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