<br>

SQL transactions are a fundamental concept in database management systems (DBMS) that allow you to group multiple SQL operations into a single, atomic unit of work. Transactions ensure the integrity, consistency, and reliability of database operations, especially in multi-user and concurrent environments. Transactions are typically managed using Transaction Control Language (TCL) commands.

## Commands

- `BEGIN` or `START TRANSACTION`: Starts a new transaction.

- `COMMIT`: Commits/saves the changes of a successful transaction.

- `SAVEPOINT`: Sets a point within a transaction to which you can later rollback if needed, without rolling back the entire transaction.

- `ROLLBACK`: Used to undo the changes done by the transaction.


