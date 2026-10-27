<details><summary>Learning Objectives</summary>

<br>

After completing this module, associates should be able to:

- Define what the `INSERT` keyword accomplishes
- Implement the `INSERT` keyword in SQL commands

</details>
<details><summary>Description</summary>
<br>

`INSERT` is an SQL command used to add a new record to the table within your database. `INSERT` statements only accept the data that follows the rules defined during the creation of your table structure. The inserted data must satisfy all constraints and match the appropriate data types; otherwise, you will encounter an error. `INSERT` is always followed by the `INTO` keyword as well.

</details>
<details><summary>Real World Application</summary>
<br>

Every company requires the persistence of information. Whenever new products are added to an e-commerce website, the business will need the ability to add all of the details for each product into their database. They must maintain data consistency when applying their products to their database to capture the appropriate metrics for a successful business. These `INSERT` commands into their products table will follow the rules of the established table to prevent any data inconsistency.

</details>
<details><summary>Implementation</summary> 
<br>

- Basic `INSERT` command syntax is as follows:

```sql
INSERT INTO TABLE_NAME (column1, column2, columnN)
VALUES (value1, value2, valueN);
```

- Example of `INSERT` command:

```sql
INSERT INTO products (product_id, p_name, quantity, p_description, category_id)
VALUES (42, 'Supercomputer: Deep Thought', 1, 'Answers the ultimate question of Life, the Universe and Everything', 7);
```

</details>
<details><summary>Summary</summary> 
<br>

The `INSERT` command is used to add any record to a table as long as that information follows the constraints and data types applied to each of the columns.
- Syntax: 
    ```sql
    INSERT INTO TABLE_NAME (column1, columnN)
    VALUES (value1, valueN);
    ```

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
