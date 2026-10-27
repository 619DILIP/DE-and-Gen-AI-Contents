
## Transaction Isolation Level

- __Read Uncommitted__ is the lowest isolation level where one transaction may read not yet committed changes made by other transactions, preventing isolation from each other.

- __Read Committed__ guarantees that any data queried is committed at the moment it is read and transaction holds a read or write lock on the current record, preventing other transactions from reading, updating, or deleting that record.

- __Repeatable Read__ is the most restrictive isolation level that holds read locks on all records it references and writes locks on referenced records for update and delete actions

- __Serializable__ is the highest isolation level to be an execution of operations in which concurrently executing transactions appears to be serially executing.


## Transaction Phenomena

- __Dirty Read__  is a situation when a transaction reads data from another transaction that has not yet been committed. 

- __Non Repeatable__ read occurs when a transaction reads the same record twice and gets a different value each time. 

- __Phantom Read__ occurs when two of the same queries are executed, but the records retrieved by the two, are different. 


