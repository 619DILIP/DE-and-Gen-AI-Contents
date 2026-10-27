<br>

- The `DEFAULT` constraint is made use of to set a default value for a column.
- The `DEFAULT` value will be added to all new records, if no other value is specified.
- The `DEFAULT` values are typically literal constants, there's an important exception for timestamp and datetime columns. Many database systems allow the use of functions like now(), CURRENT_TIMESTAMP, or similar to set the default value to the current time for these specific column types. This is a commonly used feature and an exception to the general 'literal constant' rule.
- Use `ALTER TABLE table_name  ALTER COLUMN col_name SET DEFAULT` to create a `DEFAULT` constraint to an existing column of a table.
- Use `ALTER TABLE table_name ALTER COLUMN col_name DROP DEFAULT` to delete a `DEFAULT` constraint from an existing column of a table.

