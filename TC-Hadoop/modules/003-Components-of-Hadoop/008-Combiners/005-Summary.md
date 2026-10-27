## Summary

- Combiners are just like reducers that works on the map side. They took the output of mapper and applies shuffling and sorting on the <key,value> pair. 

- They helps in reducing the network cogestions while transferring data from mapper to reducer. They are optional and are independent from map-reduce job. There is no guarantee that combiner will execute each time during map-reduce task. 

- Combiners if used efficiently will play key role in MapReduce and if not can cause the risk of expensive disk IO.

---
