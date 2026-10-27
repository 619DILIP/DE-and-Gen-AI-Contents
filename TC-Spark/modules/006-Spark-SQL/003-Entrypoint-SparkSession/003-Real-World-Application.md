### Scenario: E-commerce Analytics

An e-commerce company processes daily transaction logs stored in
distributed storage and maintains product data in Hive.

Using SparkSession:

``` python
spark = SparkSession.builder     .appName("EcommerceAnalytics")     .enableHiveSupport()     .getOrCreate()

transactions = spark.read.csv("/data/transactions.csv", header=True)

transactions.createOrReplaceTempView("transactions")

daily_sales = spark.sql("""
    SELECT product_id, SUM(amount) as total_sales
    FROM transactions
    GROUP BY product_id
""")

daily_sales.write.mode("overwrite").saveAsTable("daily_sales_summary")
```

In this workflow, SparkSession acts as:

-   The entry point to distributed processing
-   The SQL execution engine
-   The bridge to Hive
-   The configuration controller