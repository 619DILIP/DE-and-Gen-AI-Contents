<br>

- A SQL subquery is a query nested inside of a larger query. A subquery can occur in various subsections of a query:

    - SELECT clause (Inner Query)
    - WHERE clause (Nested Query)
    - FROM clause (Inline View)

- Subqueries can be nested in a `SELECT`, `INSERT`, `UPDATE`, `DELETE`, or even inside of another subquery.
- Logical operators can be used to compare the results of the subquery
- Nested queries can return single or multiple rows
- Inline views create temporary tables
- Inner queries create temporary columns on the result set
    - The column created by the inner query has a value equal to the result of the query
- The subquery can also be called `inner query` or `inner select` while the container query is called the `outer query` or `outer select`
- The `inner query` executes before the `outer query`
- Subqueries are convenient, but perform worse than joins.



