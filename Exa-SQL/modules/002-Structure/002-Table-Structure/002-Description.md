<br>

- In MySQL, a table stores and organizes data in columns and rows as defined during table creation.
- The `CREATE TABLE` command is used to create a new table in a database.
- The `DROP TABLE` command is used to completely remove the table from database.
- The `TRUNCATE TABLE` command is used to remove all the data and not the table itself.
- The `ALTER TABLE` command is used to alter the table.

- The major differences between a database and a table are as follows:

    - Tables are a way to represent the division of information in a database while, database is a collection of tables and records.
    - Tables are used to group the records in relation with each other and create a dataset. This dataset will be used in the database. The data which are stored in the table in any form is a part of the database, but the vice-versa is not true.

- `TUPLE` - A tuple refers to an ordered set of values. The number of values, or elements, in a tuple is fixed and is known as the arity of the tuple (arity - refers to number of columns in a table). Each value in the tuple is often called an attribute or a component.

In the context of databases and relational database management systems (RDBMS), a tuple is equivalent to a row in a table. Each tuple represents a single record, and the values in the tuple correspond to the attributes or columns of that record.

For example, consider a simple table representing employees:

Employee Table

| EmployeeID | FirstName | LastName | Age | Salary |
|------------|-----------|----------|-----|--------|
| 1          | Susie     | Que      | 30  | 50000  |
| 2          | Billy     | Bob      | 25  | 60000  |
| 3          | Bacon     | Hamburger| 35  | 75000  |

In this table, each row is a tuple. For instance, the first tuple (or row) is (1, "Susie", "Que", 30, 50000), where each value corresponds to a specific attribute such as EmployeeID , FirstName, LastName, Age, and Salary.

Tuples are used in various areas of computer science, including databases, programming languages, and mathematical modeling, where the concept of an ordered set of values is fundamental.