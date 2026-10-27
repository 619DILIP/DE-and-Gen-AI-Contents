## Summary

- Operations on RDD are of two types, Transformation and Action. Transformations are the operations that is used for manipulating the dataset and its return type is always a RDD. Action operations on the other hand are used for computing all the RDD at once after applying all the transformations. Their return type is always a non-rdd value. 

- Transformations can be categorized between narrow and wide transformation. Narrow transformations are those which do not result in shuffling of data whereas, wide transformations always result in shuffling of data over the network.

- Some examples of transformations are map(), filter(), groupByKey(), repartition(), etc. Some examples of actions are reduce(), collect(), take(), first(), etc.

---
