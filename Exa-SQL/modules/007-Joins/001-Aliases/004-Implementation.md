<br>

Table 1: Plants
|plant_id|plant_name   |species                          |price|
|--------|-------------|------------------------|------|
| 1           |Venus Flytrap|Dionaea muscipula                 |19.99|
| 2           |Pitcher Plant|Nepenthes                                |29.99|
| 3           |Sundew       |Drosera                                      |14.99|
| 4           |Cobra Plant     |Darlingtonia californica         |24.99|


Table 2: Customers

|customer_id|first_name|last_name|email                       |purchased_plant_id|
|-----------|----------|---------|----------------------------|------------------|
|         1|John      |Wheeler  |john.wheeler@example.com    |                 3|
|         2|Jane      |Smith    |jane.smith@example.com      |                 4|
|          3|Sussie    |Halloween|sussie.halloween@example.com|                 1|


In this example we will have two tables `Plants` and `Customers` . The `Plants` table will contain information about the plants and the `Customers` table will contain information about the customer. The `Customers` table has a `purchased_plant_id` column, which is a foreign key referencing the `plant_id` in the `Plants` table.



In SQL, column aliases are used to provide a different name for a column in the query result. This is helpful for clarity and readability. In our case, we'll use a column alias to associate purchased plants with customers in the query result.

```sql
SELECT customer_id, first_name, last_name, email,
plant_name AS purchased_plant
FROM customers 
JOIN plants  ON customers.purchased_plant_id = plants.plant_id;
```

The keyword `AS` is used to create an alias named `purchased_plant` for the column `plant_name`. This way, when you read the query, it's clear that the `plant_name` column is being displayed as `purchased_plant`. This demonstrates alias by column.

Another method for creating an alias is on the table itself. The same query as above can be used to illustrate how this works.

```sql
SELECT cust.customer_id, cust.first_name, cust.last_name, cust.email,
plnt.plant_name AS purchased_plant
FROM customers cust
JOIN plants plnt  ON cust.purchased_plant_id = plnt.plant_id;
```

Notice how after `customers` there is the abbreviation `cust`. This is to tell the editor that we are giving an alias to the `Customers` table.
The same can be said in the query about `plants` being abbreviated to `plnt`. Also, notice how the alias is used throughout the entire query. That is important as, if you are going to use a table alias, then it must be used throughout the entire query.
This however, is not the only way to write this and get the same result. Some developers find it clearer to write the same query as follows:

```sql
SELECT cust.customer_id, cust.first_name, cust.last_name, cust.email,
plnt.plant_name AS purchased_plant
FROM customers AS cust
JOIN plants AS plnt  ON cust.purchased_plant_id = plnt.plant_id;
```

Something to keep in mind is that `plant_name` is a column in the table with the alias of `purchased_plant` while `customers` has an alias of `cust` which is referring to the `Customers` table and `plants` has an alias of `plnt` which is referring to the `Plants` table. 

It is extremely common to see alias used in SQL queries as they help prevent ambiguity especially in larger databases where the same data may be in multiple tables. By providing aliases for tables and columns, developers make their queries more readable which helps avoid naming conflicts, and enhance overall code clarity.

Aliases are especially useful when dealing with complex joins or subqueries involving multiple tables, as they help distinguish between different instances of the same table and make the code more maintainable. In some cases aliases are required or the query will not work. 

**OUTPUT**: 

|customer_id|first_name|last_name|email                       |purchased_plant|
|-----------|----------|---------|----------------------------|---------------|
|          1|John      |Wheeler  |john.wheeler@example.com    |Sundew         |
|         2|Jane      |Smith    |jane.smith@example.com      |Cobra Plant    |
|         3|Sussie    |Halloween|sussie.halloween@example.com|Venus Flytrap  |