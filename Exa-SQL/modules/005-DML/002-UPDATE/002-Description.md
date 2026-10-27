<br>

`UPDATE` statements allow us to modify existing records within a table. The `UPDATE` makes use of locks on each record while modifying the table and once the row is modified the lock is released, allowing for either single or multiple record changes with a single command. 
- NOTE: Be mindful and careful when you leverage `UPDATE` statements as they do not require a `WHERE` clause. Omission of the `WHERE` clause results in all records within the table being updated.

