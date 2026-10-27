# Summary

- atomicity is combining all statements into a single unit.
  - if a database crashes for some reason, atomicity makes sure that the entire transaction is rolled back and partial results are not updated in the database
- Consistency is important to maintain data integrity, a database should consistent before and after a transaction.
  - All inconsistent data is removed, and all transactions that might cause inconsistency are aborted and an error is created or transcribed into an error log.
- Isolation is a property that guarantees the individuality of each transaction, and prevents them from being affected from other transactions. 
  - It ensures that transactions are securely and independently processed at the same time without interference, but it does not ensure the order of transactions.
- In DBMS, durability ensures that the data changes caused by the successful execution of a transaction become permanent in the database. 
  - The durability of the data is so permanent that even if the system fails or leads to a crash, the database still survives and the changes of a transaction are updated in the database.
- The ACID property of DBMS plays a vital role in maintaining the consistency and availability of data in the database.
