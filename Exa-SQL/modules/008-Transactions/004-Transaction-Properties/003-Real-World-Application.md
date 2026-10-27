# Real World Application

Please review how each of these properties can affect real-world applications

## Atomicity
A bank transaction of debiting 100$ from ACC1 and crediting it to ACC2  should be atomic, if either of the statements in this transaction fails, the transaction of transferring funds from ACC1 to ACC2 should be failed.

## Consistency
Consider two bank accounts ACC1 and ACC2 with funds of 10000$ and 9000$, which is is total of 19000$, after a transaction of transferring 50$ from ACC2 to ACC1 the funds in ACC1 is 10050$ and ACC2 are 8950$, which means the totals funds in AC1 and ACC2 adds up to 19000, So the funds in ACC1 and ACC2 are consistent before and after the Transaction.

## Isolation
Consider that the user A withdraws $100 and user B withdraws $250 from user ACC1 account, which has a balance of $1,000. Since both A and B draw from ACC1 account, one of the users is required to wait until the other user transaction is completed, avoiding inconsistent data.

## Durability
Any real life changes made to any database like transferring funds, crediting or debiting funds, updating employee details and updating grades of a student, etc are durable. once these transactions are successfully executed, the changes made to the database are permanent even if an unexpected system failure or an error occurs.