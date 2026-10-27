# Cumulative for the Mapper, Intermediate, and Reducer topic
<details><summary>Learning Objectives</summary>

After completing this module, associates should be able to:
- Know some basics of the mapper–intermediate–reducer flow
- Understand how and why it’s used
- Know what the mapper/intermediate/reducer phases are and some applications they are used for.
</details>
<details><summary>Description</summary>

# Introduction 

MapReduce is a programming model for data processing. It is simple, yet not too simple to express useful programs. MapReduce programs are inherently parallel, thus putting very large-scale data analysis into the hands of anyone with enough machines at their disposal. MapReduce comes into its own for large datasets. Each phase has key-value pairs as input and output, the types of which may be chosen by the programmer. 
It works by breaking the processing:
1. Mapper
2. Reducer 

It works by breaking processing into three phases: the map phase, the shuffle/sort phase, and the reduce phase.
reduce phase. 
1. Mapping Phase 
2. Shuffling Phase
3. Reducer Phase 

## 1. Mapper 

It will process each input record and it generates new <key, value> pairs. It can be completely different from the input pair. In mapper task, the output collects from key, value pairs. Before using the output for each mapper task, partitioning of output takes place on the basis of the key and then sorting is done.

The framework expects <key, value> pairs; input is converted to that form before the mapper runs.

### Key-Value Pair generated 

- InputSplit – Basically it is the logical representation of data. An InputSplit describes a unit of work that contains a single map task in a MapReduce program. 
- RecordReader – works with the InputSplit and converts data into <key, value> pairs suitable for the mapper. In many cases, TextInputFormat is used for converting data into the key-value pair. 

## 2. Reducer

It is used to process the output of the mapper. After processing the data,it will produce a new set of outputs. After that, HDFS stores this output data.
It uses a set of intermediate key-value pair which is produced by the mapper as the input and runs a Reducer function on each of them.

Phases of the reducer:- Shuffle Phase
- Sort Phase
- Reduce Phase

Example: Mapper Intermediate Reducer
![Example](Images/Mapper.PNG)
</details>
<details><summary>Real World Application</summary>

- Nowadays companies who are dealing with Big Data are using MapReduce for data processing. It can include processing of movie data, world population data, in counting of votes, etc.

</details>
<details><summary>Summary</summary> 

- MapReduce is a pattern as well as programming model within the Hadoop framework which is used to access big data stored in the Hadoop File System (HDFS). It is a core component, integral to the functioning of the Hadoop framework.
- It works by breaking the processing:
1. Mapper
2. Reducer 

It works by breaking processing into three phases: the map phase, the shuffle/sort phase, and the reduce phase. reduce phase. 
1. Mapping Phase 
2. Shuffling Phase
3. Reducer Phase 

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
