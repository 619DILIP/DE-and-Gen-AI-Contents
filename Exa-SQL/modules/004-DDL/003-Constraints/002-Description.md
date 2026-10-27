<br>

SQL constraints are used to help validate data beyond just a simple data type. Below is a set of commonly used SQL constraints.

| Constraint   | Use                                                                       |
| ------------ | ------------------------------------------------------------------------- |
| Not Null     | Ensures that a column's value is not null.                                |
| Unique       | Ensures that a column's value is unique in the table.                     |
| Primary Key  | Combines `unique` and `not null`. Uniquely identifies each row.           |
| Foreign Key  | Links to a row in another table. Prevents the destruction of those links. |
| Default      | Specifies a value for a column, if one is not given.                      |
| Check        | Ensures the value of a column satisfies a specific condition.             |


Each column of a table can use a combination of these constraints, but some are mutually exclusive in some vendors or context. For instance:

* Although it is possible to define both NOT NULL and DEFAULT constraints for a column, they serve distinct purposes. The DEFAULT constraint provides a fallback value when no explicit value is provided, while NOT NULL ensures that NULL values are never inserted. Using both together ensures that the column always contains a valid value.
* `DEFAULT` with a `CHECK` constraint might lead to conflicting requirements. 
* Since a `FOREIGN KEY` constraint establishes a relationship between two tables based on the values of a column in both tables, using a `CHECK` constraint to enforce similar conditions is redundant. 
* Lastly, a `PRIMARY KEY` constraint implies that a column (or a set of columns) is both `UNIQUE` and `NOT NULL` . Therefore, explicitly adding a `UNIQUE` constraint to the same column is redundant.

Constraints are used to define a database schema and are the backbone for defining `integrity constraints` of the schema. `Integrity constraints` are rules or conditions defined on a database schema to maintain the accuracy, consistency, and reliability of data within a database.
`Integrity constraints` collectively help maintain the quality and reliability of data in a database, preventing errors, inconsistencies, and ensuring that data remains meaningful for the applications and users interacting with the database. They play a crucial role in upholding the integrity of the data model and supporting data accuracy and reliability. 

