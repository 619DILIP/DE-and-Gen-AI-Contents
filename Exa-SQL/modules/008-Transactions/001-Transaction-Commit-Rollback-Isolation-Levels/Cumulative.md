<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:
- Define the isolation levels for transactions.
- Understand the importance of transactional integrity.
- Explain the transaction phenomena.

</details>
<details><summary>Description</summary>
<br>

## Transaction Isolation Levels
Isolation levels are the degree to which a transaction must be isolated from the data modifications made by any other transaction in the database system. The higher the degree of isolation, the more concurrency anomalies are prevented. However, this also means that the higher the degree of isolation, the less concurrent transactions become, which can impact performance.

### Read Uncommitted 
- Read Uncommitted is the lowest isolation level. 
- One transaction may read changes made by other transactions that have not yet been committed (transactions are not isolated from each other in any way).
- Transaction phenomena allowed: dirty read, non-repeatable read, phantom read.
- Transaction phenomena prevented: none.

### Read Committed 
- Guarantees that any data queried has already been committed.
- The transaction holds a read or write lock on the current record, preventing other transactions from reading, updating, or deleting that record.
- Transaction phenomena allowed: non-repeatable read, phantom read.
- Transaction phenomena prevented: dirty read.

### Repeatable Read 
- Prevents other transactions from updating or deleting any data it queries.
- The transaction holds read locks on all records it references and write locks on referenced records for update and delete actions.
- Transaction phenomena allowed: phantom read.
- Transaction phenomena prevented: dirty read, non-repeatable read.

### Serializable 
- Serializable is the highest isolation level. 
- It guarantees that transactions are serializable.
- Defined as an execution of operations in which concurrently executing transactions appear to be serially executing.
- Transaction phenomena allowed: none.
- Transaction phenomena prevented: dirty read, non-repeatable read, phantom read.

## Transaction Phenomena
Transaction phenomena, or concurrency anomalies, are unwanted or unexpected occurrences that can arise due to concurrent transactions being executed.

### Dirty Read 

- Dirty read is a situation when a transaction reads data from another transaction that has not yet been committed. 
    - Example:
        - Transaction 1 updates a record and leaves it uncommitted.
        - Transaction 2 queries the updated record. 
        - If transaction 1 rolls back the change, transaction 2 will have queried data that never existed.

### Non-repeatable Read 

- Non-repeatable read occurs when a transaction reads the same record twice and gets a different value each time. 
    - Example:
        - Transaction 1 queries data. 
        - Due to concurrency, Transaction 2 updates the same data and commits.
        - If transaction 1 re-queries the same data, it will retrieve a different value.

### Phantom Read 
- Phantom read occurs when two identical queries are executed, but the records retrieved by the two differ. 
    - Example:
        - Transaction 1 retrieves a set of records that satisfy a query's conditions.
        - Transaction 2 generates some new records that match the query's conditions for transaction 1. 
        - If transaction 1 re-queries the records, it gets a different set of records this time.

|Isolation Level|Dirty Reads|Non-repeatable Reads|Phantoms|
|-|-|-|-|
|Read Uncommitted|May occur|May occur|May occur|
|Read Committed|Don't occur|May occur|May occur|
|Repeatable Read|Don't occur|Don't occur|May occur|
|Serializable|Don't occur|Don't occur|Don't occur|
</details>
<details><summary>Real World Application</summary>

# Advantages 

- Improve concurrency by allowing multiple transactions to run concurrently without the risk of interfering with one another.
- Provide control over the level of data consistency required by a particular application.
- Reduce phenomena such as dirty reads, non-repeatable reads, and phantom reads.
- Provide flexibility in designing applications that require different levels of data consistency.

# Disadvantages 

- Increase overhead because the database management system must perform additional checks and acquire more locks.
- Some isolation levels can decrease concurrency by requiring transactions to acquire more locks, which can lead to blocking.
- Can limit the portability of applications across different systems, as not all RDBMS support isolation levels.
- Adds complexity to the design of database applications, making them more difficult to implement and maintain.
</details>
<details><summary>Implementation</summary> 
<br>

Let's provide examples of each isolation level and possible anomalies that might occur in a concurrent system. We'll use the following table:

```sql
CREATE TABLE users (
        id INTEGER PRIMARY KEY,
        name VARCHAR(50),
        age INTEGER
);

INSERT INTO users VALUES(1, 'Sandy', 40), 
                        (2, 'Jared', 32),
                        (3, 'Paco', 18),
                        (4, 'Derrick', 25);
```

## Read Uncommitted

#### Set Isolation Level

```sql
"SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;"
```

#### Transaction 1
```sql
BEGIN;
SELECT age FROM users WHERE id = 2; -- 32
-- other operations... transaction 2's UPDATE statement executes, even if its COMMIT statement hasn't executed
SELECT age FROM users WHERE id = 2; -- 21
COMMIT;
```

#### Transaction 2
```sql
BEGIN;
UPDATE users SET age = 21 WHERE id = 2;
-- other operations...
COMMIT;
```
A dirty read occurred. The second transaction's `UPDATE` statement had yet to be committed. This can cause an inconsistency if the update is rolled back.

## Read Committed

#### Set Isolation Level

```sql
"SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;"
```

#### Transaction 1
```sql
BEGIN;
SELECT age FROM users WHERE id = 2; -- 32
-- other operations... transaction 2's UPDATE statement and COMMIT statement execute
SELECT age FROM users WHERE id = 2; -- 21
COMMIT;
```

#### Transaction 2
```sql
BEGIN;
UPDATE users SET age = 21 WHERE id = 2;
-- other operations...
COMMIT;
```
A non-repeatable read occurred. Although the update was committed successfully and was intended, the same query resulted in different results within the same transaction. If we were making a decision in our transaction that depended on there being a consistent value for the user's age, we might not get the results we expect.

## Repeatable Read

#### Transaction 1
```sql
BEGIN;
SELECT age FROM users WHERE id = 2; -- 32
-- other operations... transaction 2 can start execution...
SELECT age FROM users WHERE id = 2; -- 32
COMMIT; -- ...however, the UPDATE statement cannot execute until this transaction finishes due to the lock on the record.
```

#### Transaction 2
```sql
BEGIN;
UPDATE users SET age = 21 WHERE id = 2;
-- other operations...
COMMIT;
```
In this example, the first transaction has a lock on the record with an id of `2`. It isn't until the first transaction ends that the second transaction can execute its `UPDATE` statement and the rest of its transaction. Notice that transaction 2 can still execute concurrently and is only blocked when it tries to interact with the same record as the first transaction.

An issue with this isolation level is that it does not prevent phantom reads, where the number of records returned from a query may differ. For example:

#### Transaction 1
```sql
BEGIN;
SELECT * FROM users WHERE age BETWEEN 10 AND 30; -- this should return records with ids of 2, 3, and 4.
-- other operations... transaction 2 executes
SELECT * FROM users WHERE age BETWEEN 10 AND 30; -- this should return records with ids of 2, 3, 4, and 5.
COMMIT;
```

#### Transaction 2
```sql
BEGIN;
INSERT INTO users VALUES (5, 'Jenny', 20);
-- other operations...
COMMIT;
```
During the execution of transaction 1, the second transaction executed completely and inserted a record that will change the number of records returned from the query in transaction 1.

## Serializable

#### Transaction 1
```sql
BEGIN;
SELECT * FROM users WHERE age BETWEEN 10 AND 30; -- this should return records with ids of 2, 3, and 4.
-- other operations... 
SELECT * FROM users WHERE age BETWEEN 10 AND 30; -- this should return records with ids of 2, 3, and 4.
COMMIT; -- Only after transaction 1 finishes does transaction 2 begin.
```

#### Transaction 2
```sql
BEGIN;
INSERT INTO users VALUES (5, 'Jenny', 20);
-- other operations...
COMMIT;
```

In this isolation level, transactions are completely isolated from one another, ensuring that transactions execute as if they were serialized one after the other. This level provides the highest degree of isolation and prevents all concurrency anomalies. However, it may lead to increased contention and decreased concurrency due to locking.

</details>
<details><summary>Summary</summary> 

## Transaction Isolation Level

- __Read Uncommitted__ is the lowest isolation level where one transaction may read changes made by other transactions that have not yet been committed, preventing isolation from each other.

- __Read Committed__ guarantees that any data queried is committed at the moment it is read, and the transaction holds a read or write lock on the current record, preventing other transactions from reading, updating, or deleting that record.

- __Repeatable Read__ is the most restrictive isolation level that holds read locks on all records it references and write locks on referenced records for update and delete actions.

- __Serializable__ is the highest isolation level, defined as an execution of operations in which concurrently executing transactions appear to be serially executing.

## Transaction Phenomena

- __Dirty Read__ is a situation when a transaction reads data from another transaction that has not yet been committed. 

- __Non-repeatable read__ occurs when a transaction reads the same record twice and gets a different value each time. 

- __Phantom Read__ occurs when two identical queries are executed, but the records retrieved by the two differ. 

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
