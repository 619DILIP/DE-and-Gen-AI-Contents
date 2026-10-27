<br>



## Transaction Isolation Levels
Isolation levels are the degree to which a transaction must be isolated from the data modifications from any other transaction in the database system. The higher the degree of isolation, the more concurrency anomalies are prevented. However, this also means that the higher the degree of isolation, the less concurrent transactions become and this can impact performance.

### Read Uncommitted 
- Read Uncommitted is the lowest isolation level 
- One transaction may read not yet committed changes made by other transactions (transactions are not isolated from each other in any way)
- Transaction phenomena allowed: dirty read, non-repeatable read, phantom read
- Transaction phenomena prevented: none

### Read Committed 
- Guarantees that any data queried has already been committed
- Transaction holds a read or write lock on the current record, preventing other transactions from reading, updating, or deleting that record.
- Transaction phenomena allowed: non-repeatable read, phantom read
- Transaction phenomena prevented: dirty read

### Repeatable Read 
- Prevents other transactions from updating or deleting any data it queries
- The transaction holds read locks on all records it references and writes locks on referenced records for update and delete actions
- Transaction phenomena allowed: phantom read
- Transaction phenomena prevented: dirty read, non-repeatable read


### Serializable 
- Serializable is the highest isolation level. 
- Guaranteed to be serializable
- Defined to be an execution of operations in which concurrently executing transactions appears to be serially executing.
- Transaction phenomena allowed: none
- Transaction phenomena prevented: dirty read, non-repeatable read, phantom read


## Transaction Phenomena
Transaction phenomena, or concurrency anomalies, are unwanted or unexpected occurrences that can occur due to concurrent transactions being executed.

### Dirty Read 

- Dirty Read is a situation when a transaction reads data from another transaction that has not yet been committed. 
    - Example:
        - Transaction 1 updates a record and leaves it uncommitted.
        - Transaction 2 queries the updated record. 
        - If transaction 1 rolls back the change, transaction 2 will have queried data that never existed.

### Non Repeatable read 

- Non Repeatable read occurs when a transaction reads the same record twice and gets a different value each time. 
    - Example:
        - Transaction 1 queries data. 
        - Due to concurrency, Transaction 2 updates the same data and commit
        - If transaction 1 re-queries the same data, it will retrieve a different value.

### Phantom Read 
- Phantom Read occurs when two same queries are executed, but the records retrieved by the two, are different. 
    - Example:
        - Transaction 1 retrieves a set of records that satisfy a queries conditions.
        - Transaction 2 generates some new records that match the queries conditions for transaction T1. 
        - If transaction T1 re-queries the records, it gets a different set of records this time.


|Isolation Level|Dirty Reads|Non-repeatable Reads|Phantoms|
|-|-|-|-|
|Read Uncommitted|May Occur|May Occur|May Occur|
|Read Committed|Don't Occur|May Occur|May Occur|
|Repeatble Read|Don't Occur|Don't Occur|May Occur|
|Serializable|Don't Occur|Don't Occur|Don't Occur|