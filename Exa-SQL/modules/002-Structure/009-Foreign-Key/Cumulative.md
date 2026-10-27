<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:
- Define and implement FOREIGN KEY

</details>
<details><summary>Description</summary>

<br>

A FOREIGN KEY is a field (or collection of fields) in one table that refers to the PRIMARY KEY in another table.

</details>
<details><summary>Real World Application</summary>
<br>

Consider any database; for example, in a company database, an `employee` table has details like `id`, `name`, `branch id`, `address`, `manager id`, etc. Consider another table called `branch`, which an employee belongs to. The `branch id` in the employee table is a foreign key referencing the primary key of the `branch` table.

Similarly, consider another table called `client`, which has details like `client name`, `employee id`, etc. The `employee id` in the `client` table is a foreign key referencing the primary key of the `employee` table.

</details>
<details><summary>Implementation</summary> 
<br>

Step 1: Create a Branch and Employee table
```sql
CREATE TABLE Branch(
    id INT PRIMARY KEY,
    name VARCHAR(20)
);

CREATE TABLE Employee(
    id INT PRIMARY KEY,
    name VARCHAR(20),
    address VARCHAR(50)
);
```
Step 2: Add branch_id as a foreign key for the employee table

```sql
ALTER TABLE Employee ADD branch_id INT;
ALTER TABLE Employee ADD FOREIGN KEY (branch_id) REFERENCES Branch(id);
```
```sql
DESC Employee;
```
Result:
| Field       | Type        | Null | Key | Default | Extra |
|-------------|-------------|------|-----|---------|-------|
| employee_id | int         | NO   | PRI | NULL    |       |
| first_name  | varchar(20) | YES  |     | NULL    |       |
| last_name   | varchar(20) | YES  |     | NULL    |       |
| emp_role    | varchar(20) | YES  |     | NULL    |       |
| branch_id   | int         | YES  | MUL | NULL    |       |

The `id` column in the `branch` table is its PRIMARY KEY, and it is used by the FOREIGN KEY of the `employee` table.

</details>
<details><summary>Summary</summary> 
<br>

- A foreign key is used to connect two or more tables so that data from both can be put to use in parallel.

- A foreign key is a field or collection of fields in a table that refers to the primary key of another table. It is responsible for managing the relationship between the tables.

- The table that contains the foreign key is called the child table, and the table whose primary key is being referred to by the foreign key is called the parent table.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
