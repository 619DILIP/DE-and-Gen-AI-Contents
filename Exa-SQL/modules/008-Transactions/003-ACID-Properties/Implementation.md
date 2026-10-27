<br>

For the following examples consider a banking application which allows funds to transfer between accounts.

## Atomicity

Consider transferring 50$ from an account (ACC1) to another account (ACC2) where we check if ACC1 has sufficient funds.
```sql
START TRANSACTION;
UPDATE TABLE bankaccounts SET funds = funds-50 WHERE account_no= ACC1 AND funds>50;
UPDATE TABLE bankaccounts SET funds = funds+50 WHERE account_no= ACC2;
COMMIT;
```

In the above example debiting 50$ from ACC1 and crediting 50$ to ACC2 is a single transaction. If the entire transaction was not atomic, then it would be possible that our application debits ACC1 but does not credit ACC2 due to some error.

## Consistency

Building off of this example, let's examine ACC1 and ACC2

```sql
SELECT * FROM bankaccounts;
```
**RESULT**:

|account_no |funds|
|-----------|-----|
| ACC1      | 850 |
| ACC2      |1,150|

From the above table we can conclude that the sum of funds in ACC1 and ACC2 is 2000$.

Consider a transaction of transfering 150$ funds from ACC2 to ACC1.  

```sql
START TRANSACTION;
UPDATE TABLE bankaccounts SET funds = funds-150 WHERE account_no= ACC2;
UPDATE TABLE bankaccounts SET funds = funds+150 WHERE account_no= ACC1;
COMMIT;
```

```sql
SELECT * FROM bankaccounts;
```

**RESULT**:

|account_no |funds|
|-----------|-----|
| ACC1      |1,000|
| ACC2      |1,000|

From the above table it can be observed that the total funds in ACC1 and ACC2 are 2000$, from this we can conclude that the database is consistent before and after the transaction.

## Isolation

Expanding on this code, we take the following steps:

**Step 1**: create a new bank account named ACC3

```sql
INSERT INTO bankaccounts VALUES("ACC3", 1000);
```
**Step 2 (transaction 1)**: crediting 1000$ funds to ACC3

```sql
START TRANSACTION or BEGIN;
UPDATE bankaccounts SET funds=funds+1000 WHERE account_no='ACC3';
COMMIT;
```

**Step 3 (transaction 2)**: transferring 100$ from ACC2 to ACC1.

```sql
START TRANSACTION or BEGIN;
UPDATE bankaccounts SET funds=funds-100 WHERE account_no='ACC2';
UPDATE bankaccounts SET funds=funds+100 WHERE account_no='ACC1';
COMMIT;
```
In the above example, transaction 1 and transaction 2 are concurrent, as we are affecting different accounts with each update statement.

## Durability

Let's look at a database before and after a successful transaction:
```sql
SELECT * FROM banckaccounts;
```
|account_no |funds|
|-----------|-----|
| ACC1      |1,100|
| ACC2      |  900|
| ACC3      |1,000|

```sql
START TRANSACTION or BEGIN;
UPDATE bankaccounts SET funds=funds+100 WHERE account_no='ACC3';
COMMIT;
```

```sql
SELECT * FROM banckaccounts;
```  

|account_no |funds|
|-----------|-----|
| ACC1      |1,100|
| ACC2      |  900|
| ACC3      |1,100|

From the above example, it can be observed that the results of the transaction, which is crediting 100$ to ACC3 are successfully updated into the database.

