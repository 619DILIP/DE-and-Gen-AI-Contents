RDD Transformations are operations that create a new RDD from an
existing RDD.

Key Properties:

- RDDs are immutable (original data is never modified).
- Transformations are lazy (execution happens only after an action).
- Spark builds a Directed Acyclic Graph (DAG) of transformations.
- Execution is optimized before running.

## Types of Transformations

### 1. Narrow Transformations

- No data shuffle required
- Faster execution
- Data stays within partitions

Examples: - map() - filter() - flatMap() - mapValues()

### 2. Wide Transformations

- Require shuffle across partitions
- More expensive operations
- Network communication involved

Examples: - groupByKey() - reduceByKey() - distinct() - repartition() -
intersection() - sortBy()

Choosing the correct transformation directly impacts performance.