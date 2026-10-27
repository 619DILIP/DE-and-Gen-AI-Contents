# Introduction

It is an optimization technique in Spark SQL that uses buckets and bucketing columns to determine data partitioning.
Which is used as unethical practice whereby a broker generates a profit by misleading their client about the execution of a particular trade. Basically,  Bucketing  refers to a situation in which the broker confirms that a requested trade has taken place without actually executing that order.

Example :

- A bucket is a round and deep container used for carrying things. 
- A bucket is what you'd use to carry water from a faucet to a kiddie pool.
- A basket (Basketball) .

It is a technique in Spark which used to optimize the performance of the task. In bucketing clustering columns(buckets) determine data partitioning and prevent data shuffle. Which is based on the value of one or more bucketing columns, the data is allocated to a predefined number of buckets.

![Bucketing](Images\Bucket.png)

Once we start using a bucket, we need to specify the number of the buckets for the bucketing column (column name). Once the specification of bucket is done then its time for loading, the data processing engine will calculate the hash value for that column, based on which it will reside in one of the buckets. 

Bucketing has two key benefits:

- Improved query performance
- Improved sampling







