<br>

In SQL, `CASCADE` is a keyword used to simultaneous delete or update data from both the child and parent tables and is used in conjunction while writing the query with `ON DELETE` or `ON UPDATE`. Applying `CASCADE` keyword to the command applies the changes in both parent and child tables accordingly to the execution of that query. `CASCADE` is appended to the reference command for the foreign key when creating a table.

## ON DELETE

Appending `ON DELETE CASCADE` to the foreign keys within our child table allow us the opportunity to delete the parent record and subsequently delete all relational information in any referenced table through one command. Otherwise, due to referential integrity it would require multiple commands to delete all of the referenced records inside of the child tables first, before removing the parent record.

## ON UPDATE

Appending `ON UPDATE CASCADE` to the foreign key within our child table allows us to update information in a singular command by updating the parent table record will apply to all subsequent child tables information. This also helps reduce the amount of commands and keeps our referential integrity intact.