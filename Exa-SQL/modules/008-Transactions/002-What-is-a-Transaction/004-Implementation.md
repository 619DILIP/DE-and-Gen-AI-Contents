
## SQL Transactions 

Consider an example where there’s a `bankaccounts` table and we are doing an intra-bank transfer, i.e. person holding account `ACC1` is trying to transfer $100 to account  `ACC2`.

Step 1: Create Table `bankaccount` with columns `account_no` and `funds`.
``` sql
CREATE TABLE bankaccounts(
    account_no varchar(20) PRIMARY KEY NOT NULL,
    funds decimal(8,2)
);
```

Step 2: Add two accounts named `ACC1` and `ACC2` with an initial fund balance of $1000 each.
``` sql
INSERT INTO bankaccounts VALUES("ACC1", 1000);
INSERT INTO bankaccounts VALUES("ACC2", 1000);
```

Step 3: Now, let’s see the transaction of transfering 100$ from `ACC1` to `ACC2`.
``` sql
START TRANSACTION or BEGIN; 
UPDATE bankaccounts SET funds=funds-100 WHERE account_no='ACC1';
UPDATE bankaccounts SET funds=funds+100 WHERE account_no='ACC2';
COMMIT; 
```

