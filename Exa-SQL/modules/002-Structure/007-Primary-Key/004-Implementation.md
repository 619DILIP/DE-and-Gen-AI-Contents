<br>

Below is an example of creating a table named `employee` with `employee_id` as primary key

``` sql
 CREATE TABLE employee(
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(20),
    last_name VARCHAR(20),
    emp_role VARCHAR(20)
    );
```
``` sql
DESC employee;
```
The `DESC` or `DESCRIBE` commands describe the table.


result:
| Field       | Type        | Null | Key | Default | Extra |
|-------------|-------------|------|-----|---------|-------|
| employee_id | int         | NO   | PRI | NULL    |       |
| first_name  | varchar(20) | YES  |     | NULL    |       |
| last_name   | varchar(20) | YES  |     | NULL    |       |
| emp_role    | varchar(20) | YES  |     | NULL    |       |

