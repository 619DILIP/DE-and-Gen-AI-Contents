<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Define the `UPDATE` keyword.
- Leverage the `UPDATE` syntax in a database.
- Understand potential risks associated with the `UPDATE` statement.

</details>
<details><summary>Description</summary>
<br>

`UPDATE` statements allow us to modify existing records within a table. The `UPDATE` statement uses locks on each record while modifying the table, and once the row is modified, the lock is released, allowing for either single or multiple record changes with a single command.
- NOTE: Be mindful and careful when you leverage `UPDATE` statements, as they do not require a `WHERE` clause. Omission of the `WHERE` clause results in all records within the table being updated.

</details>
<details><summary>Real World Application</summary>
<br>

`UPDATE` commands are constantly used to help manage employee information at both an individual record level and in bulk. For example, when HR needs to update the contact information for an employee who has changed addresses. Additionally, sometimes there is reorganization within departments, so a team might be moved to a new department, which also needs to be reflected by updating the employee's record.

</details>
<details><summary>Implementation</summary> 
<br>

- Basic syntax for implementing `UPDATE`

```sql
UPDATE TABLE_NAME
SET column1 = value1, column2 = value2, columnN = valueN
WHERE [condition];
```

- Example of `UPDATE` for a single record in an employee with id = 12 for address
    - NOTE: Double-check the ID whenever you use these commands to ensure you're updating the appropriate record.

```sql
UPDATE employees
SET add_street = 'Philly Lane', add_number = '20211', add_zip = 19101
WHERE employee_id = 12;
```

- Example of `UPDATE` for multiple records in employees to transfer department_name from "QC" to "Tech"

```sql
UPDATE employees
SET department_name = 'Tech'
WHERE department_name = 'QC';
```

</details>
<details><summary>Summary</summary> 
<br>

`UPDATE` allows us to change information for a single record or multiple records inside the tables of our database. This is an extremely important tool that also requires close attention to detail, as the omission of the `WHERE` clause or inaccuracies in the specified conditions could lead to drastic changes.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
