
## Insert

The `INSERT` command is used to store new records in a database table.

```SQL
INSERT INTO <table_name> (col1 [, col2, ...]) {VALUE | VALUES} (valuelist) [, (valuelist), ...]
```

The `INSERT` command to insert 1 or more records. Below is an example:

```SQL
INSERT INTO my_table (id, my_value, my_other_value) VALUES (1, 'some data', 1.0);
```

The results of the insert statement are the number of rows affected by the statement. The results should be:
![Single insert result](../../resources/single_insert_results.PNG)

Multiple records can be inserted using a single `INSERT` command.

```SQL
INSERT INTO my_table (id, my_value, my_other_value) VALUES (2, 'misc data', 2.0), (3, 'even data', 100.13);
```

![Multiple insert result](../../resources/multi_insert_result.PNG)

## Update

The `UPDATE` command is used to modify whole records or parts of records in a database table.

```SQL
UPDATE <table_name> SET assignment_list [WHERE where_list]
```

The `UPDATE` command can modify 0 or more records and the results of the command are the number of rows affected by the command.

```SQL
UPDATE my_table SET my_value='new value';
```

![Unfiltered update results](../../resources/unfil_update.PNG)
As you can see with the previous update statement all of the inserted rows were updated. This may or may not be your intended results.

To limit the number or rows that are updated, it is best practice to include the optional `WHERE` clause.

```SQL
UPDATE my_table SET my_value='where val' WHERE id=1;
```

![Filtered update results](../../resources/filtered_update.PNG)
Now the results of the update statement are restricted to the `WHERE` clause. Since there is only a single record with the id of 1, only that single record is updated.

## Delete

The `DELETE` command is used to remove data from a database table.

```SQL
DELETE FROM <table_name> [WHERE where_condition]
```

Much like the `UPDATE` command the `DELETE` command has an optional `WHERE` clause. However, the `DELETE` command can be very destructive, it is best practice to always have a `WHERE` clause on the statement. If you exclude a `WHERE` clause on the `DELETE` command the database will remove all records from the table.

```SQL
DELETE FROM my_table WHERE id=3;
```

The results of the `DELETE` command are the number of rows affected.
![Delete results](../../resources/delete_results.PNG)

<hr/>

## Exercise (Optional)

Using the library database and the books table from [DDL implementation](../001-DDL/Implementation.md)

- Insert 3 books into the `books` table.
- Insert a book titled, 'Learn SQL in a Snap', authored by 'Jim Dandy', published on 01-01-01
- Modify the author of the first book inserted into the database
- Delete the second and third books inserted into the database
