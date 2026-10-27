<br>

An SQL transaction is a sequence of one or more SQL operations (such as queries, inserts, updates, or deletes) that are treated as a single unit of work. Transactions are managed using Transaction Control Language (TCL) commands.
 
# Commands

1. `START TRANSACTION / BEGIN`: Starts a new transaction.

2. `COMMIT`: 
This command is used to save the data permanently. 
Whenever we perform any of the DML command like `INSERT`, `DELETE` or `UPDATE`, these can be rolled back if the data is not stored permanently. So in order to be at the safer side `COMMIT` command is used. 
 
3. `ROLLBACK`: 
This command is used to get the data or restore the data to the last savepoint or last committed state. If due to some reasons the data inserted, deleted or updated is not correct, you can rollback the data to a particular savepoint or if savepoint is not done, then to the last committed state. 

4. `SAVEPOINT`: 
This command is used to save the data at a particular point temporarily, so that whenever needed can be rolled back to that particular point. 

