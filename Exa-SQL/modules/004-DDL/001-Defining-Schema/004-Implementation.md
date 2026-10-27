<br>

When working with SQL you use the keyword `CREATE` to generate a schema, along with all the other components utilized by the schema.

- Generate a new schema in SQL

```sql
CREATE SCHEMA employment;
GO
```

- Generate a table inside a specific schema

```sql
CREATE TABLE employment.employees(
    employee_id INT PRIMARY  KEY IDENTITY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department VARCHAR(50)
);
```

- Generate a view inside of a specific schema

```sql
CREATE VIEW employment.hr_employees AS
SELECT first_name, last_name
FROM employment.employees
WHERE department = 'HR';
```