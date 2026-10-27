<br>

Structured Query Language or SQL is the standard language for working with RDBM systems. SQL is used to administer and manipulate SQL servers. SQL is a scripting language that is interpreted by the database server. SQL is used to...

- Define database structure
- Manipulate stored data
- Define data access permissions
- Control concurrent data access
- Query stored data

To accomodate the operations of the above categories, SQL is broken into 5 sublanguages.

| Sublanguage | Description                                                                 |
| ----------- | --------------------------------------------------------------------------- |
| DDL         | Data Definition Language. Defines data structure                            |
| DML         | Data Manipulation Language. Insert, Update, Delete record                   |
| DCL         | Data Control Language. Grant or revoke access permissons to database object |
| TCL         | Transaction Control Language. Defines concurrent operation boundaries       |
| DQL         | Data Query Language. Search, filter, group, aggregate stored data           |

Each sublanguage is responsible for a specific set of operations and have a specific set of commands associated with them. Breaking down each sublanguage is beyond the scope of this document, but they will be discussed in more depth in their own sections.

SQL itself is generally case-insensitive, but it's a good practice to follow a consistent naming convention (e.g., always using lowercase or uppercase) for tables, columns, and other identifiers to avoid potential issues related to case-sensitivity.