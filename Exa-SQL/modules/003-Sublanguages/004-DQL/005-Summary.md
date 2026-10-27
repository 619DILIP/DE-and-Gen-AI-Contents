<br>

The SQL DQL sublanguage is the backbone for querying a database for data. The command set is simple consisting of the single `select` command. However, The sublangage is built on a grammar structure that is used to:

- Search data
- Project record views
- Filter records
- Group values
- Offset resultsets

The `select` statement is the crux of the DQL sublanguage and is composed of clauses that determine how records are selected from the database.

| Phrase  | Clause 1                   | Clause 2                |
| ------- | -------------------------- | ----------------------- |
| Search  | ... FROM table_ref         |                         |
| Project | SELECT col_1 [, col_2] ... |                         |
| Filter  | WHERE where_condition      |                         |
| Group   | Group By group_list        | Having having_condition |
| Offset  | Limit count                | Offset count            |
