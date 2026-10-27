<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:
- Describe the purpose of a function in a database.
- Create, execute, and delete a function.

</details>
<details><summary>Description</summary>
<br>

A function in SQL serves a similar purpose to functions in dedicated programming and scripting languages. It performs a defined set of operations on given data and returns a result. Functions in SQL are similar to procedures except that functions return a value.

When creating a function, we provide a definition of what our function has to do. We must call the function to perform the defined task as needed. When a program calls a function, program control is switched to that function.

- Characteristics of a function include:
    - Functions are separate blocks mainly used for calculations or bundling common operations into a single call.
    - Functions with DML commands can be called from other blocks, but functions without DML commands are typically called using a SELECT query.
    - Arguments (input values) can be passed into functions when called by defining function parameters during function creation.
      - These parameters should be included in the calling statements.
    - A function uses the RETURN command to return a value or raise an exception. 
      - The RETURN command is mandatory to create SQL functions, as it will always return a value; in calling statements, it is always accompanied by an assignment operator to populate the variables.

Many SQL dialects and RDBMSs provide built-in functions for convenience; however, the creation of custom functions may be helpful to support a developer's specific database operations.

</details>
<details><summary>Real World Application</summary>
<br>

Real-world applications include:

- Development of a password strength function.
- Maintenance of student or bank account details.
- Accessing and modifying data in a directory.

</details>
<details><summary>Implementation</summary> 
<br>

Functions are created using the DML command `CREATE`. For the following examples, we are showcasing MySQL, but many SQL dialects support the creation of functions.

## Syntax for creating a function

The following showcases the typical structure of a function using the `CREATE` command.

```sql

CREATE FUNCTION function_name [ (parameter datatype [, parameter datatype]) ]
RETURNS return_datatype
BEGIN

   -- declaration_section

   -- executable_section

END;
```

Notice that `BEGIN` and `END` are used to declare the operations for the function. Additionally, the `RETURNS` keyword is used to define the type of data returned from the function. Similar to other functions, optional parameter lists can be declared for the function to be later referenced within the function's operations.

- Example:

The SQL statement below creates the function get_balance:

```sql
DELIMITER //

CREATE FUNCTION get_balance(acc_no INT)
RETURNS INT
DETERMINISTIC
BEGIN
   DECLARE acc_bal INT;
   
   SELECT order_total 
   INTO acc_bal 
   FROM sample2.orders 
   WHERE customer_id = acc_no 
   LIMIT 1;
      
   RETURN acc_bal;
END//

DELIMITER ;
```

In this example, the `get_balance` function is used to find the value of the `order_total` column for a specified `customer_id` (based on the input `acc_no` argument) from a table called `orders`. `DELIMITER //` is used to change the delimiter temporarily, so that semicolons within the procedure do not end the `CREATE PROCEDURE` statement prematurely. `DELIMITER ;` resets the delimiter back to the default semicolon.

## Syntax for executing a function

The following query showcases how to execute the function. Here, we are locating the `order_total` from the account `101`.

```sql
SELECT get_balance(101);
```

Output:
```
4700
```

## Syntax for deleting a function

The SQL statement below showcases the syntax to `DROP` a previously created function. An optional `IF EXISTS` statement can be added to the `DROP` command to check for the existence of the function prior to deletion. This can be helpful to avoid errors.

```sql
DROP FUNCTION [ IF EXISTS ] function_name;
```

Here, we see the syntax to drop the previously created `get_balance` function.

```sql
DROP FUNCTION IF EXISTS get_balance;
```

</details>
<details><summary>Summary</summary> 
<br>

- SQL functions perform a defined set of operations on given data and return a result.
- They can have parameters.
- A function uses the RETURN command to return a value or raise an exception, and the RETURN command is mandatory.
- Many SQL dialects and RDBMSs provide built-in functions for convenience; however, the creation of custom functions may be helpful to support a developer's specific database operations.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
