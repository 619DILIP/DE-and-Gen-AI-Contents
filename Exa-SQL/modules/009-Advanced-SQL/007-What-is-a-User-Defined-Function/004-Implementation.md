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

The SQL statement below creates the function get_balance

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

In this example the `get_balance` function is used to find the value of the `order_total` column for a specified `customer_id` (based on the input, `acc_no` argument) from a table called `orders`. `DELIMITER //` is used to change the delimitor temporarily, so that semicolons within the procedure do not end the `CREATE PROCEDURE` statement prematurely. `DELIMITER ;` resets the delimiter back to the default, semicolon.

## Syntax for executing a function

The below query showcases how to execute the function. Here, we are locating the `order_total` from the account `101`.

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
