<br>

Syntax to create a table with employee_id as an attribute which will `AUTO_INCREMENT` on inserting new record.

``` sql
CREATE TABLE table_name(
variable_name variable_datatype AUTO_INCREMENT
);
```

Example:

``` sql
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    employee_name VARCHAR(50),
    department_id INT
);
```

This same table written using `SERIAL` would look as follows:

```sql
CREATE TABLE table_name (
    variable_name SERIAL PRIMARY KEY,
    -- Other columns...
);
```

Example:

```sql
CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    employee_name VARCHAR(50),
    department_id INT
);
```

Notice the syntactical differences between the two table queries. This example is why it is important to always refer to documentation when working with different dialects of SQL. 

You can modify auto incremented values, however, it is highly discouraged as the value is automatically managed by the system and should represent a unique identifier for each row. 
