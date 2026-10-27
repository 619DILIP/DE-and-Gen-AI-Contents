Understanding RDD operations is critical in real-world scenarios such
as:

## Log Analysis

-   filter() to extract error logs
-   map() to format log entries
-   count() to compute total errors

## Word Count Application

-   flatMap() to split lines into words
-   map() to assign count 1 to each word
-   reduceByKey() to aggregate word frequencies

## Data Aggregation

-   groupByKey() or reduceByKey() to compute totals
-   collect() or saveAsTextFile() to retrieve final results

Choosing narrow transformations when possible improves performance.