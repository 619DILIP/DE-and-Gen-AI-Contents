<br>

* The `UNIQUE` constraint is used to ensure every value of a column is different. This means that each row must have a distinct value in the specified column.

* The `UNIQUE` key interacts with NULL values somewhat, unintuitively, so let’s dive deeper into this.

    A `UNIQUE` key allows for `NULL` column values for records.

    There is often confusion around how many `NULL` values a `UNIQUE` constraint can have in a column. Each database may have slight differences in the amount of `NULL` values that are allowed with a `UNIQUE` constraint. Some database systems only allow a single `NULL` value; however, databases often allow multiple `NULL` values.

    In other words, when a column is declared as `UNIQUE` and allows `NULL`, the `UNIQUE` constraint applies only to the non-null values. Rows with `NULL` values in that column are not considered duplicates in terms of the `UNIQUE` constraint. This is because `NULL` is actually the absence of a value. However, keep in mind that each non-null value must still be unique across all rows.

    It's essential to consult the documentation of the specific database system you are using to understand its behavior regarding `UNIQUE` constraints and `NULL` values. Always consider the unique constraints enforced by your database to ensure the correct behavior based on your requirements. 

    Keep in mind that a column can have multiple constraints applied to it. The UNIQUE constraint ensures that all values in the column are distinct. However, in most databases, UNIQUE does not prevent multiple NULL values since NULL is treated as an unknown value. To ensure that no NULL values exist in a column, use the NOT NULL constraint in combination with UNIQUE.
