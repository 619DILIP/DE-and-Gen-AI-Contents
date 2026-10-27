<br>

Subqueries are queries that are contained in another query. The container query is known as the `outer query` and the subquery is known as the `inner query`. There are 3 types of subqueries

- Nest Query in the `WHERE` clause
- Inline View in the `FROM` clause
- Inner Query in the `SELECT` clause

Important Notes

- Nested queries can return single or multiple rows
- Nested query results can be compared using logical operators
- Inline views create temporary tables
- Inner queries create temporary columns on the result set
- The column created by the inner query has a value equal to the result of the query

Subqueries are convenient, but perform worse than joins.
