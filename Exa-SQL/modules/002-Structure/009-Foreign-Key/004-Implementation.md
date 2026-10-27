<br>

Step 1: Create a Branch and Employee table
``` sql
CREATE TABLE Branch(
    id INT PRIMARY KEY,
    name VARCHAR(20)
     );

CREATE TABLE Employee(
    id INT PRIMARY KEY,
    name VARCHAR(20),
    address VARCHAR(50)
     );
```
Step 2: Add branch_id as foreign key for employee table

``` sql
ALTER TABLE employee ADD branch_id INT;
ALTER TABLE employee ADD FOREIGN KEY (branch_id) REFERENCES Branch(id);
```
``` sql
 DESC employee;
 ```
 Result:
| Field       | Type        | Null | Key | Default | Extra |
|-------------|-------------|------|-----|---------|-------|
| employee_id | int         | NO   | PRI | NULL    |       |
| first_name  | varchar(20) | YES  |     | NULL    |       |
| last_name   | varchar(20) | YES  |     | NULL    |       |
| emp_role    | varchar(20) | YES  |     | NULL    |       |
| branch_id   | int         | YES  | MUL | NULL    |       |

The `id` column in the `branch` table is its PRIMARY KEY and it is used by the FOREIGN KEY of the `employee` table.


