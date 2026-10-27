<br>

`DELETE` is a keyword command in SQL used to remove a specific record from a table or relation. The `DELETE` command, generally, includes a `WHERE` clause to specify the records for deletion. 
- However, much like the `UPDATE` command there is a risk that if the `WHERE` clause is not specified it will remove all records from the table. 
- The `DELETE` command removes one record at a time and logs each deleted row.
    - This why it's not considered good practice to delete all records in a table using `DELETE` when you want to maintain the table structure. 
    - `TRUNCATE` offers a better solution for deleting all records from a table as it's both faster and removes the data by deallocating the data pages used to store the records. 
- `DELETE` commands can also activate a trigger and work with indexed views.