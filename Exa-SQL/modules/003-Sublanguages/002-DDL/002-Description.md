<br>

Data Definition Language is the SQL language subset used for defining data or altering structure in the database.

In order to utilize the functions of the DDL sublanguage, a database user must have the appropriate permissons on the server and on the particular parent object. For instance, to create a table on a database, the user must have the permission to create the table on the database object. That same user may not have any other permissions on the same parent object.

### Commands

- CREATE
- DROP
- ALTER
- RENAME
- TRUNCATE
- COMMENT

### Create

The `CREATE` command is used to create objects on the server. `CREATE` can be used to create:

- Database
- User
- Table
- Index
- Trigger
- Function
- Stored Procedure
- View

### Drop

The `DROP` command is used to remove objects from the server. Any object created using the `CREATE` command can be dropped using the `DROP` command.

### Alter

The `ALTER` command is used to change some characteristics of an object. The command will ultimately be used to add, drop, or modify some option on the object.

The `ALTER` command is commonly used to change table characteristics, like:

- Add/Drop columns
- Add/Drop constraints
- Modify column data types
- Modify column constraints

### Rename

The `RENAME` command is used to rename objects.<br>
NOTE: The availability and syntax of the `RENAME` command for database objects vary between database management systems (DBMS). Consult the specific DBMS documentation to ensure accurate command usage 

### Truncate

The `TRUNCATE` command is used to remove all data from a table along with all space allocated for the records. Unlike `DROP` truncate will preserve the structure of the table.

### Comment
The `COMMENT` command is typically used to add comments or descriptions to database objects like tables, columns, or views. This information is not used by the database itself but can be helpful for documentation purposes or for providing additional information about the structure of the database.
You could also write comments in SQL by using single line `--` and multi-line `/*  */` comments.
