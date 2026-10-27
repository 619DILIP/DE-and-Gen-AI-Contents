<br>

Constraints are tied directly to the table and define the integrity of the data as part of the schema. Administrators use constraints to apply database level validation according to application and database requirements.

Table 1: Vendor

```sql
CREATE TABLE Vendor(
 vendorId  CHAR(2) NOT NULL,
 vendorName VARCHAR(25) UNIQUE NOT NULL,
 PRIMARY KEY (vendorId)
); 
```


This table demonstrated the `NOT NULL`, `PRIMARY KEY`, and `UNIQUE` constraints

Table 2: SalesTransaction

```sql
CREATE TABLE SalesTransaction(
 transId VARCHAR(8) PRIMARY KEY,
 customerId CHAR(7) NOT NULL REFERENCES Customer(customerId),
 storeId INT NOT NULL REFERENCES Store(StoreId),
-- Using DEFAULT to default to the current date cannot be null because a default value will be given
 transDate DATE DEFAULT now()
);
```

The above table demonstrated the use of `PRIMARY KEY`, `NOT NULL`, `FORIEGN KEY`, and `DEFAULT` constraints.