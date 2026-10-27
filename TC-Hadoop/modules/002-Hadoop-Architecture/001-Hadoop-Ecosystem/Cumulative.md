# Cumulative for the Hadoop Ecosystem topic
<details><summary>Learning Objectives</summary>

- Understand the architecture of Hadoop

</details>
<details><summary>Description</summary>

## Description

- Hadoop follows a master-slave architecture in which the master consists of NameNode and resource manager and the slave consists of DataNode, node manager and map-reduce phases. 

- The NameNode and DataNode are the part of HDFS(Hadoop Distributed File System), the resource manager and node manager are the part of YARN(Yet Another Resource Negotiator) and Map and Reduce Phase are the part of Map-Reduce Framework. 

### Hadoop Architecture Components  
<br> 
  
![Hadoop](Image/architecture1.PNG)    

- **MasterNode:** It is the main node of the system which keeps information of NameNode, journal node and job trackers. Without it any processing cannot be done in Hadoop. 

- **NameNode:** It is responsible for managing and maintaining the file system namespace including files and directories present in DataNode. 

- **DataNode:** It is the place where actual data is stored in HDFS. Each DataNode can store multiple data blocks of default size 128mb. 

- **Resource Manager:** It consists of two things, one is Job Tracker which resides in master node and is responsible for accepting map-reduce jobs from clients and process that data with the help of NameNode. The second one is Task Tracker which resides in the slave node and receives the task send by job tracker and performs processing on those task. 

- **Map Reduce Framework:** This framework works in two phases one in Map phase also called as Mapper and another one is Reduce phase also known as Reducer. The mapper takes the input from HDFS, process it and send the output of map phase to the reducer. The reducer's input is the output of map phase and it further applies some processing on the input and send the final outcome to the master node. 

---
</details>
<details><summary>Real World Application</summary>

## Real World Example

- Big Companies like Google, Oracle and Facebook are following the hadoop architecture and using it's Map reduce component for processing of huge volume of data. 

- Marks and Spencer, one of the luxury brands, is using Hadoop's HDFS for maintaining and storing customer related data that helps them to do analytics on it to make decisions which targets the customers on the large scale. 

---
</details>
<details><summary>Implementation</summary> 

</details>
<details><summary>Summary</summary> 

## Summary 

- Hadoop is the framework to store and process the data and for doing so it follows a Master Slave architecture. 

- The masternode is responsible for stabilizing parallel processing of data, resource allocation for the task and receives the information sent by slave nodes. 

- The slavenode is responsible for storing the data, maintaining and processing it using map-reduce. 

- All these things makes hadoop a complete open source framework to handle big data under its hood. 

---
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
