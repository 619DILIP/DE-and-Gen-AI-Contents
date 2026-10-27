<br>

`CREATE`
- It is part of the DDL sublanguage
- `CREATE` is a command that creates new database objects, like tables, in the database
- Tables are used to store the data in the database with a unique name and schema
    - tables also require at least one column to be valid
    - Each column requires an associated data type
- Certain RDBMS have transactional DDL language that allows you to rollback creates
    - PostgreSQL, SQL Server and SQLite among various others have transactional DDL
    - MySQL and Oracle Database do not support transactional DDL
- Used to also define schemas, procedures, views, indexes and even databases

`DROP`
- It is part of the DDL sublanguage
- The `DROP` command removes the table from the database.
- It removes all the indexes, privileges, rows and frees the memory space for other objects.
- You can not drop the table referenced by foreign key constraint.
- The objects related to the table like views, procedures needs to be explicitly dropped.
- No DML triggers will be fired.
- We can not roll back the drop table operation.

`TRUNCATE`
- It is part of the DDL sublanguage
- It is used to remove all the rows from the table.
- It does not return number of rows truncated from the table.
- It also deallocates the memory for that object and other object will use that deallocated space.
- `TRUNCATE` operation can not roll back as it does not operate on each row.
- We cannot use condition when it comes to using `TRUNCATE`.


