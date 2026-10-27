<details><summary>Learning Objectives</summary>

<br>

After completing this module, associates should be able to:
- Define all CRUD Operations
- Understand which SQL commands are associated with each operation
- Implement the use of each of these

</details>
<details><summary>Description</summary>

<br>

CRUD operations are the foundation of any computer programming language that is based on the four operations used to implement persistent storage for applications such as a relational database. These operations are not strictly for SQL but can also be utilized by NoSQL. CRUD stands for the following:
- **C**reate: `CREATE` & `INSERT` commands from SQL allow us to facilitate this operation.
- **R**ead: `SELECT` command from SQL allows us to facilitate this operation.
- **U**pdate: `UPDATE` command from SQL allows us to facilitate this operation.
- **D**elete: `DELETE` command from SQL allows us to facilitate this operation.

</details>
<details><summary>Real World Application</summary>
<br>

You cannot interact with databases without using CRUD operations as they are essential for anything requiring persistent storage. Even web developers wouldn't be able to use REST, a superset of CRUD, to access HTTP requests and responses. CRUD is also crucial for the end-user to perform actions on the site they are visiting, creating bookmarks and interacting with others on the internet. CRUD operations help businesses facilitate control of security by satisfying various access requirements and simplify design to allow for more scalability and better performance.

</details>
<details><summary>Implementation</summary> 
<br>

- Basic syntax for **C**reate operations you've seen previously:

```sql
CREATE TABLE TABLE_NAME (
    col_1 INT PRIMARY KEY, 
    col_2 VARCHAR(20), 
    col_N INT
);

INSERT INTO TABLE_NAME (column1, column2, columnN)
VALUES (value1, value2, valueN);
```

- Basic syntax for **R**ead operations you've seen previously:

```sql
SELECT * FROM TABLE_NAME;

SELECT col_1, col_N
FROM TABLE_NAME
WHERE id = 1;
```

- Basic syntax for **U**pdate operations you've seen previously:

```sql
UPDATE TABLE_NAME
SET column1 = value1, column2 = value2, columnN = valueN
WHERE [condition];
```

- Basic syntax for **D**elete operations you've seen previously:

```sql
DELETE FROM TABLE_NAME
WHERE [condition];
```
</details>
<details><summary>Summary</summary> 
<br>

Understanding CRUD operations allows developers to build powerful web applications that can persist and retrieve information rapidly and easily from a database.

CRUD:
- **C**reate: `CREATE` & `INSERT` commands from SQL allow us to facilitate this operation.
- **R**ead: `SELECT` command from SQL allows us to facilitate this operation.
- **U**pdate: `UPDATE` command from SQL allows us to facilitate this operation.
- **D**elete: `DELETE` command from SQL allows us to facilitate this operation.
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
