<br>

Consider an example of a transaction where you tried to add a new bank account ACC3 and set the funds to 10000. In that same transaction, you tried to create another account, ACC4, and set its funds to 900000 when it was supposed to be 9000. If the entire transaction is rolled back, the step of creating ACC3 with 10000 initial funds would also be rolled back. To avoid this, a save point can be added soon after creating ACC3 and we can roll back to before the statement of that creates account ACC4.

``` sql
START TRANSACTION;
INSERT INTO bankaccounts VALUES("ACC3", 10000);
SAVEPOINT sv;
INSERT INTO bankaccounts VALUES("ACC4", 900000);
ROLLBACK TO sv;
INSERT INTO bankaccounts VALUES("ACC4", 90000);
COMMIT;
```
