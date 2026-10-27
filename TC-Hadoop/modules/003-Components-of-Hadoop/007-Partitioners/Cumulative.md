# Cumulative for the Partitioners topic
<details><summary>Learning Objectives</summary>

- To understand the work of partitioner. 

</details>
<details><summary>Description</summary>

- A partitioner plays an important role in-between mapper and reducer. It takes the intermediate output from all the mappers and partition it based on the key, typically using a hash function. 
- Same keys from different mappers are grouped together by the partitioner and it stores them in a single partition. 
- It reduces the chances of getting incorrect results from the reducers as it sends same keys to same reducer. 

### Some Questions related to partitioners 

**Ques:** When partitioner can be created in map-reduce task? 
- **Ans:** Partitioning only matters when you have more than one reducer; with a single reducer, all keys go to one partition.

**Ques:** How to decide the number of partitioners in the MapReduce job? 
- **Ans:** It can be decided based on the number of reducers used. The number of partitions equals the number of reducers. 

**Ques:** What are the types of partitioners? 
- **Ans:** Partitioners are of two types:   
i) *Default Partitioner:* It uses the hash function to distribute same keys in the same partition based on the hash value.    
ii) *Custom Partitioner:* These are the user defined partitioners that stores the result in different reducers based on the condition given by the user. 

**Ques:** Which method is used to control the number of partitioners in Hadoop?
- **Ans:** `Job.setNumReduceTasks(int)` method is used to control the number of partitioners.

**Ques:** Which method to use for creating custom partitioner in Hadoop?
- **Ans:** To create a custom partitioner for your map-reduce job, implement the `getPartition(K key, V value, int numPartitions)` method that takes two parameters, one is key-value pair and another one is the number of partitions.

**Ques:** What is the need of Partitioners in Hadoop MapReduce?
- **Ans:** The partitioners will help in reducing the processing of same key data by different reducers which may result in wrong outcome.

---

</details>
<details><summary>Real World Application</summary>

- Big Data analyst creates the custom partitioner whenever the same key fields are more in number for reducing the processing time of same key fields by different reducers. 

- Companies are using data partitioner to segregate the related data into one partition.

</details>
<details><summary>Implementation</summary> 

- Let's assume that we have a dataset of world_population in which there are 4 fields id, country, state and population_count. Our Sample data look like this,

```
id,country,state,population_count
001,USA,Texas,2345677
002,USA,NY,5555555
003,India,Delhi,301111111
```

- This dataset is sent to mapper function which tokenizes each field using delimiter as comma(,). 
- Now to create a partition, we are writing a script in Hadoop using the id and country field both as the key so that those same keys will be sent to same reducers, which results in more accurate output. 
- We are using the `KeyFieldBasedPartitioner` of Hadoop, that allows us to partition the map output based on certain key(s). For example: 

```
Hadoop jar Hadoop-streaming-2.5.2.jar \
    -D stream.map.output.field.separator=, \
    -D stream.num.map.output.key.fields=4 \
    -D map.output.key.field.separator=,\
    -D MapReduce.partition.keypartitioner.options=-k1,2 \
    -D MapReduce.job.reduces=3 \
    -input myInputDirs \
    -output myOutputDir \
    -mapper /bin/cat \
    -reducer /bin/cat \
    -partitioner org.apache.Hadoop.mapred.lib.KeyFieldBasedPartitioner

```

- Here, the `-D stream.map.output.field.separator` and `map.output.key.field.separator` both specifies the separator for the partition which is comma(,). 
- Here, `-D stream.num.map.output.key.fields=4` option will store the first 4 fields as a key of map and rest other line as its value. If the line does not have any fields after fourth "," then an empty string object ("") will get assigned as a value.  
- The `D MapReduce.partition.keypartitioner.options=-k1,2` option will partition the map output by first two fields of the keys, i.e, id and country in our case. This also ensures that key/value pairs having the first two fields same are sent to same reducer. 
- The sample partition data after executing the above script will look something like this: 

```
part-00001

001,USA,Texas,2345677
002,USA,NY,5555555
------------------------

part-00002

003,India,Delhi,301111111

```

--- 
</details>
<details><summary>Summary</summary> 

- Partitioners are used when there are number of same key fields present in the mapper output. They are used to partition the output of mapper function and stores all the same key into same part files.
- The Partitioner numbers in the map-reduce job can be decided on the basis of reducer count in the job. The number of partitioners are equal to number of reducers. 
- We can either use the default partitioner that is there in Hadoop's library or we can create a custom partitioner based on our own condition. These partitioners helps in getting more accurate result from the reducers as the same key fields are processed by the same reducer only. 

---

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
