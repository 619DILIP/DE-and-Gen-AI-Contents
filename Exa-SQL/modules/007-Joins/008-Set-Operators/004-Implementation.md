<br>

This example will use two tables, `businesses` and `sales`:

**Table 1**: businesses

|business_id|business_name        |
|-----------|---------------------|
|          1|Fashion Excess Cloths|
|          2|High Fashion Shoes   |



**Table 2**: sales 

|sale_id|business_id|product_id|quantity|total_amount|
|-------|-----------|----------|--------|------------|
|      1|          1|       101|       3|      300.00|
|      2|          1|       102|       2|      200.00|
|      3|          2|       101|       5|      500.00|
|      4|          2|       103|       4|      400.00|


## UNION 

The SQL `UNION` operator merges the result sets of multiple SELECT statements into a single result set, removing duplicates. Ensure that the number and data types of columns in the SELECT statements match to avoid errors; for instance, a SELECT with 2 columns cannot be combined with another having 3 columns.


```sql
-- UNION: Get a combined list of all unique products sold across businesses
SELECT product_id
FROM (
    SELECT product_id FROM sales
    WHERE business_id IN (SELECT business_id FROM businesses)
    UNION
    SELECT product_id FROM sales
) AS union_result;
```
A list of unique `product_id` values that have been sold across all businesses. Duplicates are automatically removed by UNION .

The subquery before `UNION` selects the products with the product_id of 101, 102, and 103. The result of `UNION` will remove duplicates, so the output will be: 101, 102, 103.

**OUTPUT**:

|product_id|
|----------|
|       102|
|       101|
|       103|


If you wanted to include duplicate values you could use `UNION ALL`. 
```sql
-- UNION ALL: Get a combined list of all products sold across businesses (including duplicates)
SELECT product_id
FROM (
    SELECT product_id FROM sales
    WHERE business_id IN (SELECT business_id FROM businesses)
    UNION ALL
    SELECT product_id FROM sales
) AS union_all_result;
```
`UNION ALL` differs from `UNION` in that it does not remove duplicate rows; it includes all rows from the combined result sets.

The subquery before `UNION ALL` selects products with the product_id of 101, 102, and 103.

**OUTPUT**:

|product_id|
|----------|
|       101|
|       102|
|       101|
|       103|
|       101|
|       102|
|       101|
|       103|



## INTERSECT

The `INTERSECT` operator in SQL is used to retrieve the common rows that appear in the result sets of two SELECT statements. It returns only the distinct rows that exist in both result sets.

NOTE: MySQL **does not** support the `INTERSECT` clause. Achieve similar functionality using `INNER JOIN` or `IN` clauses. Always refer to the database documentation to ensure the correct usage of these clauses.

```sql

-- INTERSECT: Get a list of products sold in common across all businesses
SELECT product_id
FROM (
    SELECT product_id FROM sales
    WHERE business_id = 1
    INTERSECT
    SELECT product_id FROM sales
    WHERE business_id = 2
) AS intersect_result;
```
The subqueries selects the products with the `product_id` of 101. The result of `INTERSECT` will include `product_id` 101, which is common to both businesses.


**OUTPUT**:

|product_id|
|----------|
|       101|





## EXCEPT

The `EXCEPT` operator in SQL is used to retrieve the rows that are present in the result set of the first SELECT statement but not in the result set of the second SELECT statement. It returns the distinct rows from the first result set that do not appear in the second result set. 


```sql
-- EXCEPT: Get a list of products sold in the first business but not in the second business
SELECT product_id
FROM (
    SELECT product_id FROM sales
    WHERE business_id = 1
    EXCEPT
    SELECT product_id FROM sales
    WHERE business_id = 2
) AS except_result;
```

The first subquery selects `product_id` 101 and 102. While the second subquery selects `product_id` 101.The result of `EXCEPT` will exclude product_id 102, which is sold in the first business but not in the second.



**OUTPUT**:

|product_id|
|----------|
|       102|



Note that the `MINUS` clause, found in some databases, is functionally equivalent to the `EXCEPT` clause. For example, in PostgreSQL or Oracle, you can replace `EXCEPT` with `MINUS` in your queries. Always refer to the database documentation to ensure the correct usage of these clauses.
