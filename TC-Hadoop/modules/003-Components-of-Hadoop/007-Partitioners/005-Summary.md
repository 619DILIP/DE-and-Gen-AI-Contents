## Summary

- Partitioners are used when there are number of same key fields present in the mapper output. They are used to partition the output of mapper function and stores all the same key into same part files.

- The Partitioner numbers in the map-reduce job can be decided on the basis of reducer count in the job. The number of partitioners are equal to number of reducers. 

- We can either use the default partitioner that is there in hadoop's library or we can create a custom partitioner based on our own condition. These partitioners helps in getting more accurate result from the reducers as the same key fields are processed by the same reducer only. 

---

