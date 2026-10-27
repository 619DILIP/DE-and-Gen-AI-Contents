<br>

Stored Procedures are created using the DML command `CREATE`. For the following examples, we are showcasing MySQL, but many SQL dialects support the creation of stored procedures. The exact syntax may vary from Language-to-Language.

## Syntax for creating a procedure

```sql
CREATE PROCEDURE procedure_name ( IN | OUT | INOUT parameter_name parameter_datatype, … )
BEGIN    
    -- SQL statements
END
```

Note: MySQL allows data to be returned from a Stored Procedure using the `OUT` or `INOUT` declaration for parameters. This functionality is not supported in all SQL dialects.

### Example

The following showcases how to create a procedure named UpdateEmployeeSalaries which will update the Salary column of all records in an Employees table based on a PercentageIncrease argument given.
```sql
DELIMITER //

CREATE PROCEDURE UpdateEmployeeSalaries(IN PercentageIncrease DECIMAL(5,2))
BEGIN
    -- Updating the salaries
    UPDATE Employees
    SET Salary = Salary * (1 + PercentageIncrease / 100);

    -- Logging the update
    INSERT INTO SalaryUpdateLog (UpdateDate, PercentageIncrease)
    VALUES (NOW(), PercentageIncrease);
END //

DELIMITER ;
```

Let’s break down this example in more detail:

* `DELIMITER //` is used to change the delimiter temporarily, so that semicolons within the procedure do not end the `CREATE PROCEDURE` statement prematurely.
* This procedure takes a single input parameter, PercentageIncrease which is a `DECIMAL` datatype. This decimal can include up to 5 digits and has a precision (numbers to the right of the decimal point) of two decimal places.
* `BEGIN` marks the start of the procedure statements and END marks the end of the procedure.
* The `UPDATE` statement sets the salary of all employees in the Employees table to a new value increased by the PercentageIncrease argument passed when calling this procedure.
* The `INSERT` statement records a log in a SalaryUpdateLog table which includes the date of the update and the argument given for the PercentageIncrease parameter.
* Finally, `DELIMITER ;` resets the delimiter back to the default, semicolon.

To call this procedure, using MySQL, you would use the keyword `CALL`.
```sql
CALL UpdateEmployeeSalaries(3.0)
```
## Syntax for deleting a procedure

DDL is also used to remove the procedure. As such, the DROP command can be used to remove a previously created stored procedure.

```sql
DROP PROCEDURE [IF EXISTS] stored_procedure_name;
```

Note: The brackets around `IF EXISTS` means that the operators are optional, and will check if the entity exists prior to completing the rest of the operation. In the example below you will see it used with and without:

To remove the UpdateEmployeeSalaries procedure, the syntax would look like this:
```sql
-- Remove the Procedure 'UpdateEmployeeSalaries' if it exists.
DROP PROCEDURE IF EXISTS UpdateEmployeeSalaries; 
```
alternatively:
```sql
-- Remove the Procedure 'UpdateEmployeeSalaries'. May throw an error is the procedure does not exist.
DROP PROCEDURE UpdateEmployeeSalaries;
```
