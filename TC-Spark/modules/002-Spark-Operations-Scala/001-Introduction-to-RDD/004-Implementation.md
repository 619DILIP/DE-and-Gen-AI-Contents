## Implementation

As we already talked about the several ways of creating a RDD in Spark. Let us now see how to create them. 

**1. Creating RDD using `parallelize()` method**

- To create an RDD, first we must import Spark classes.

```
import org.apache.spark.SparkContext
import org.apache.spark.SparkConf
```

- Then create `SparkConf` and `SparkContext` object.

```
val conf = new SparkConf().setMaster(master).setAppName(app_name)

val sc = new SparkContext(conf) 

```
**Note:** 
> `setMaster()` and `setAppName()` are the minimum properties required to run spark application.

- Now, we can use parallelize() over 3 types of collection, array, sequence and list. We will see each other one by one. 
  - **Creating RDD on Array Collection**
  ```
  val data = Array(1,2,3,4,5)
  val arr_rdd = sc.parallelize(data)
  ```

  - **Creating RDD on Sequence Collection**
  ```
  val data = Seq(1,2,3,4,5)
  val sequence_rdd = sc.parallelize(data)
  ```

  - **creating RDD on List Collection**
  ```
  val data = List(1,2,3,4,5)
  val list_rdd = sc.parallelize(data)
  ```

- The work of parallelize() is to distribute data of specified collection on multiple nodes of a cluster so that processing of data would happen in parallel which results in fast outcome. 


**2. Creating RDD from Existing RDD**

- When we apply any transformation operation on existing RDD, then a new RDD has been created. For example, we are going to apply `map()` function on existing RDD "rdd1".
```
val rdd1 = sc.parallelize(Array(1, 2, 3)) 

val rdd2 = rdd1.map(sum => sum+1)
rdd2.collect
```

- Here, `collect` is an action applied on rdd2 to get all the elements in output screen.

**Note:**
> We will discuss more about RDD operations in Basic-RDD-Operations module. 


**3. Creating RDD from existing Dataframe or Dataset** 

- To convert any Dataframe or Dataset to RDD, simply add `rdd` to it. For Example, let's assume we have a Dataframe as "df" and we want to convert it into RDD. To do so must write...
```
val demo_rdd = df.rdd
```

**Note:** 
> In "Data-Load-Store" module, we will be seeing how to create a RDD from referencing a dataset.

---

