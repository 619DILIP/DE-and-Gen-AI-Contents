<br>

Let's do examples of each isolation level and possible anomalies that might occur in a concurrent system. We'll use the following table:

```sql
create table users (
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
"SET TRANSACTION ISOLATION LEVEL READ COMMITTED;"
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
COMMIT; -- ...however the UPDATE statement cannot execute until this transaction finishes due to the lock on record
```


#### Transaction 2
```sql
BEGIN;
UPDATE users SET age = 21 WHERE id = 2;
-- other operations...
COMMIT;
```
In this example, the first transaction has a lock on the record that has an id of `2`. It isn't until the first transaction ends that the second transaction can execute its `UPDATE` statement and the rest of its transaction. Notice that transaction 2 can still execute concurrently and is only blocked when it tries to interact with the same record as the first transaction.

An issue with this isolation level is that it does not prevent phantom reads, which is where the number of records returned from a query may differ. For example:


#### Transaction 1
```sql
BEGIN;
SELECT * from users WHERE age BETWEEN 10 AND 30; -- this should return records with ids of 2, 3, and 4
-- other operations... transaction 2 executes
SELECT * from users WHERE age BETWEEN 10 AND 30;-- this should return records with ids of 2, 3, 4, and 5
COMMIT;
```


#### Transaction 2
```sql
BEGIN;
INSERT INTO users VALUES (5, 'Jenny', 20);
-- other operations...
COMMIT;
```
During the execution of transaction 1, the second transaction executed completely and inserted a record that will change the amount of records returned from the query in transaction 1.

## Serializable

#### Transaction 1
```sql
BEGIN;
SELECT * from users WHERE age BETWEEN 10 AND 30; -- this should return records with ids of 2, 3, and 4
-- other operations... 
SELECT * from users WHERE age BETWEEN 10 AND 30;-- this should return records with ids of 2, 3, and 4
COMMIT; -- Only after transaction 1 finishes does transaction 2 begin
```


#### Transaction 2
```sql
BEGIN;
INSERT INTO users VALUES (5, 'Jenny', 20);
-- other operations...
COMMIT;
```

In this isolation level, transactions are completely isolated from each other, ensuring that transactions execute as if they were serialized one after the other. This level provides the highest degree of isolation and prevents all concurrency anomalies. However, it may lead to increased contention and decreased concurrency due to locking.
