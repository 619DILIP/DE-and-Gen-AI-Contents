<br>

Here's an example SQL `CREATE TABLE` statement that demonstrates the use of various common data types:

```SQL

CREATE TABLE Employee (
    EmployeeID INT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Gender CHAR(1),
    DateOfBirth DATE,
    Salary DECIMAL(10, 2),
    IsManager BOOLEAN,
    DepartmentID INT,
    JoinDate TIMESTAMP
);

```

Let's explain the columns in this example:

- EmployeeID: INT data type is used for storing integer values.
- FirstName and LastName: VARCHAR data type is used for storing variable-length character strings.
- Gender: CHAR data type is used for storing single-character values.
- DateOfBirth: DATE data type is used for storing date values.
- Salary: DECIMAL data type is used for storing fixed-point numbers with precision and scale.
- IsManager: BOOLEAN data type is used for storing boolean values (true or false).
- DepartmentID: INT data type is used for storing integer values.
- JoinDate: TIMESTAMP data type is used for storing date and time values.