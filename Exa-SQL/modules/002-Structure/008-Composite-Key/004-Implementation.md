<br>

Below is an example of using a composite key.

## Step 1: Create the tables called employee, client, and branch.

``` sql
CREATE TABLE employee(
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(20),
    last_name VARCHAR(20),
    manager_id INT,
    FOREIGN KEY(manager_id) REFERENCES employee(employee_id) ON DELETE SET NULL
    );
CREATE TABLE client(
    client_id INT PRIMARY KEY,
    client_name VARCHAR(20),
    branch_id INT,
    FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE SET NULL

);
CREATE TABLE branch (
  branch_id INT PRIMARY KEY,
  client_name VARCHAR(40),
  manager_id INT,
  FOREIGN KEY(manager_id) REFERENCES employee(employee_id) ON DELETE SET NULL
);
```
## Step 2: Create a table works_with

``` sql
CREATE TABLE works_with (
  employee_id INT,
  client_id INT,
  sales INT,
  PRIMARY KEY(employee_id, client_id),
  FOREIGN KEY(employee_id) REFERENCES Employee(employee_id) ON DELETE CASCADE,
  FOREIGN KEY(client_id) REFERENCES Client(client_id) ON DELETE CASCADE
);
```
In the above table `works_with`, `employee_id` and `client_id` are combined to create a composite key.
