## Description

- A partitioner plays an important role in-between mapper and reducer. It takes the intermediate output from all the mappers and partition and it is based on the keys and by a hash function. 

- Same keys from different mappers are clubbed together by the partitioner and it stores them in a single partition. 

- It reduces the chances of getting wrong result from the reducers as it sends same keys to same reducer. 

### Some Questions related to partitioners 

**Ques:** When partitioner can be created in map-reduce task? 

- **Ans:** It can be created only when there is more than one reducer in the program.

**Ques:** How to decide the number of partitioners in the map reduce job? 

- **Ans:** It can be decided based on the number of reducers used. The number of partitioner should be same as the number of reducers. 

**Ques:** What are the types of partitioners? 

- **Ans:** Partitioners are of two types:   
i) *Default Partitioner:* It uses the hash function to distribute same keys in the same partition based on the hash value.    
ii) *Custom Partitioner:* These are the user defined partitioners that stores the result in different reducers based on the condition given by the user. 

**Ques:** Which method is used to control the number of partitioners in Hadoop?

- **Ans:** `JobConf.setNumReduceTasks()` method is used to control the number of partitioners.

**Ques:** Which method to use for creating custom partitioner in Hadoop?

- **Ans:** To create a custom partitioner for your map-reduce job, implements the `getpartition()` method that takes two parameters, one is key-value pair and another one is the number of partitions.

**Ques:** What is the need of Partitioners in Hadoop MapReduce?

- **Ans:** The partitioners will help in reducing the processing of same key data by different reducers which may result in wrong outcome.

---

