## Implementation 

- Let's assume that we have a dataset of world_population in which there are 4 fields id, country, state and population_count. Our Sample data look like this,

```
id,country,state,population_count
001,USA,Texas,2345677
002,USA,NY,5555555
003,India,Delhi,301111111
```

- This dataset is sent to mapper function which tokenized each word using delimiter as comma(,). 

- Now to create a partition, we are writing a script in hadoop using the id and country field both as the key so that those same keys will be sent to same reducers, which results in more accurate output. 

- We are using the `KeyFieldBasedPartitioner` of hadoop, that allows us to partition the map output based on certain key. For example: 

```
hadoop jar hadoop-streaming-2.5.2.jar \
    -D stream.map.output.field.separator=, \
    -D stream.num.map.output.key.fields=4 \
    -D map.output.key.field.separator=,\
    -D mapreduce.partition.keypartitioner.options=-k1,2 \
    -D mapreduce.job.reduces=3 \
    -input myInputDirs \
    -output myOutputDir \
    -mapper /bin/cat \
    -reducer /bin/cat \
    -partitioner org.apache.hadoop.mapred.lib.KeyFieldBasedPartitioner

```

- Here, the `-D stream.map.output.field.separator` and `map.output.key.field.separator` both specifies the separator for the partiton which is comma(,). 

- Here, `-D stream.num.map.output.key.fields=4` option will store the first 4 fields as a key of map and rest other line as its value. If the line does not have any fields after fourth "," then an empty string object ("") will get assigned as a value.  

- The `D mapreduce.partition.keypartitioner.options=-k1,2` option will partition the map output by first two fields of the keys, i.e, id and country in our case. This also ensures that key/value pairs having the first two fields same are sent to same reducer. 

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
