# Cumulative for the Bucketing
<details><summary>Prerequisites and Learning Objectives</summary>

# Prerequisites
General experience using a computer.

# Learning Objectives
After completing this module, associates should be able to:

- Define the concept of Bucketing. 
- Describe the uses of Bucketing.
</details>
<details><summary>Description</summary>

# Introduction

Bucketing is an optimization technique in Spark SQL that uses buckets and bucketing columns to determine data partitioning. It is not to be confused with unethical practices whereby a broker generates a profit by misleading their clients about the execution of a particular trade. Essentially, Bucketing refers to a situation in which a broker confirms that a requested trade has taken place without actually executing that order.

Examples:

- A bucket is a round and deep container used for carrying things. 
- A bucket is what you would use to carry water from a faucet to a kiddie pool.
- A basket (Basketball).

Bucketing is a technique in Spark that is used to optimize performance. In bucketing, clustering columns (buckets) determine data partitioning and prevent data shuffling. Based on the value of one or more bucketing columns, the data is allocated to a predefined number of buckets.

![Bucketing](Images\Bucket.png)

Once we start using a bucket, we need to specify the number of buckets for the bucketing column (column name). Once the specification of the bucket is done, it's time for loading. The data processing engine will calculate the hash value for that column, based on which it will reside in one of the buckets. 

Bucketing has two key benefits:

- Improved query performance
- Improved sampling

</details>
<details><summary>Real World Application</summary>

# Real World Example 

Examples:

- A bucket is a round and deep container used for carrying things. 
- A bucket is what you would use to carry water from a faucet to a kiddie pool.
- A basket (Basketball).
</details>
<details><summary>Implementation</summary> 

# Implementation 

### Create a bucketed table:

        df.write\
            .bucketBy(16, 'key') \
            .sortBy('value') \
            .saveAsTable('bucketed', format='parquet')


### How to make the data bucketed

In the Spark API, we can use the function bucketBy.

        (
        df.write
        .mode(saving_mode)  # append/overwrite
        .bucketBy(n, field1, field2, field3, field4, ...)
        .sortBy(field1, field2, field3, field4, ...)
        .option("path", output_path)
        .saveAsTable(table_name)
        )
</details>
<details><summary>Summary</summary> 

# Summary 

Bucketing is a technique in Spark that is used to optimize the performance of tasks. In bucketing, clustering columns (buckets) determine data partitioning and prevent data shuffling. The data is allocated to a predefined number of buckets based on the value of one or more bucketing columns.
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
