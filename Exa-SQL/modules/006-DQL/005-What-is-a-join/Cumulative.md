<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Define what a join is.
- Understand the importance of joins in SQL.
</details>
<details><summary>Description</summary>
<br>

In relational databases, data stored in multiple tables is related to one another through a common key value. This relationship is established by a foreign key in the child table linking to the parent table. There is a constant need to extract records from related tables to obtain the full picture of the information stored in our database. After applying certain conditions, this joined information is compiled based on the type of join using SQL's `JOIN` clause. This `JOIN` clause is a part of DQL and is used in queries to access multiple tables based on the logical relationships of those tables, joining that information together in the output as a single table. Several different types of SQL `JOIN` clauses will be explained in other modules.
</details>
<details><summary>Real World Application</summary>
<br>

In businesses, when they are looking to analyze metrics for quarterly business profits, they have queries that pull information from multiple tables across their entire database. This includes joining information from sales and product data to see how much profit is being made in sales versus the cost of maintaining those products. `JOIN` clauses are frequently used to handle such tasks. Additionally, you could query and join information regarding customer orders to track which categories of products are selling the most. There is a nearly endless number of uses for `JOIN` clauses in business analytics to help improve operations as a whole.

</details>
<details><summary>Implementation</summary> 
<br>

- Basic SQL `JOIN` clause syntax, using `INNER JOIN` to demonstrate basic syntax.

```sql
SELECT 
TABLE_NAME1.column1, TABLE_NAME1.columnN, TABLE_NAME2.column1, TABLE_NAME2.columnN
FROM TABLE_NAME1
INNER JOIN TABLE_NAME2
ON TABLE_NAME1.matching_column = TABLE_NAME2.matching_column;
```

</details>
<details><summary>Summary</summary> 
<br>

This `JOIN` clause is part of DQL and is used in queries to access multiple tables based on the logical relationships of those tables, joining that information together in the output as a single table. 
- There are several different types of SQL `JOIN` clauses.
- This relationship is established by a foreign key in the child table linking to the parent table, which is used as the 'matching_column' for the join. 
- There is a constant need to extract records from related tables to obtain the full picture of the information stored in the business's database. 
- After applying certain conditions, this joined information is compiled based on the type of join using SQL's `JOIN` clause. 
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
