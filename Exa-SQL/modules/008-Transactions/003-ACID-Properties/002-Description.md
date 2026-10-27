<br>

The ACID properties are a set of four properties that guarantee the reliability and consistency of database transactions. They can be remembered using the acronym ACID: Atomicity, Consistency, Isolation, and Durability.

## Atomicity

A transaction is considered to be atomic if it cannot be further broken down into individual operations, and all of the operations that occur within a transaction either succeed or fail as a single unit. If a single operation fails during a transaction, then everything is considered to have failed and must be rolled back.

## Consistency

One of the advantages of using a transaction is that, even if the transaction is a success or a failure, the database is consistent, and the data integrity is maintained.

## Isolation

Every transaction is isolated from other transactions. Therefore, a transaction shouldn't affect other transactions running at the same time. Stated another way, data modifications made by one transaction should be isolated from the data modifications made by other transactions. So, while a transaction can see data in the state it was in before another concurrent transaction modified it, as well as after the second transaction has completed, it cannot see any intermediate states.

## Durability

Data modifications that take place within a successful transaction may be safely considered to be stored in the database regardless of whatever else may occur. As each transaction is completed, a row is entered in the database transaction log. Thus, in the event of a system failure that requires the database to be restored from a backup, you can use this transaction log to get the database back to the state it was in after a successful transaction.