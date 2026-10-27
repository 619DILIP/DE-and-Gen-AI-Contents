<br>

The DDL sublanguage of SQL is utilized to create and manage the structure of a database. DDL consists of the commands `CREATE`, `DROP`, `ALTER`, `TRUNCATE`, and `RENAME`. Using DDL the overall structure is modeled by creating objects like tables where the specific columns, data types, constraints, and relationships are defined.

The DML sublanguage of SQL is utilized to create, update, and delete data in a database. DML consist of the `INSERT`, `UPDATE`, and `DELETE` commands. Using DML, the records in database are manipulated to reflect to overall state of the applications that utilize the database for persistence.

The SQL DQL sublanguage is the backbone for querying a database for data. The command set consists of the single `SELECT` command. However, the sublangage is built on a grammar structure that is used to:

- Search data
- Project record views
- Filter records
- Group values
- Offset resultsets

The `SELECT` statement is the crux of the DQL sublanguage and is composed of clauses that determine how records are selected from the database.

| Phrase  | Clause 1                   | Clause 2                |
| ------- | -------------------------- | ----------------------- |
| Search  | ... FROM table_ref         |                         |
| Project | SELECT col_1 [, col_2] ... |                         |
| Filter  | WHERE where_condition      |                         |
| Group   | Group By group_list        | Having having_condition |
| Offset  | Limit count                | Offset count            |


The DCL sublanguage is used to `GRANT` or `REVOKE` access privileges to databases and database objects.
