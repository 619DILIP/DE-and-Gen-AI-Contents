## E-Commerce Sales Analysis

An e-commerce company stores millions of transaction records.

Each transaction may contain:

- Customer information
- Product information
- Quantity
- Price
- Transaction timestamp

A Big Data workflow can be used to calculate:

- Total sales
- Sales by product
- Most purchased products
- Customer purchase trends

A simplified architecture is:

```text
E-Commerce Transactions
          ↓
        HDFS
          ↓
       PySpark
          ↓
     DataFrame
          ↓
 Transform / Aggregate
          ↓
       Results
```

This demonstrates how distributed storage and processing technologies can work together to analyze large datasets.