<br>

- Referential integrity is the relationship between tables. Each table in a database has a primary key and this primary key can appear in other tables because of its relationship to data within other tables. When a primary key from one table appears in another table, it is called a foreign key.
- Referential integrity does not allow the addition of any record in a table that contains the foreign key unless the reference table contains a corresponding primary key.
- Referential integrity does not allow deletion of a record in a table that contains the foreign key. To delete the record in the parent table, the corresponding record in the child table should be deleted first. To solve this issue ON DELETE CASCADE is used. 
- Other options are to set the foreign key to null or to its default value (only if the default value references an existing value in the primary-key table).
