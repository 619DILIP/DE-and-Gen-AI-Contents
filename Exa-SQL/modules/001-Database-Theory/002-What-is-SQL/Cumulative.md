<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Define SQL
- Describe the purpose of using SQL
- List the SQL sublanguages

</details>
<details><summary>Description</summary>
<br>

Structured Query Language, or SQL, is the standard language for working with RDBMS systems. SQL is used to administer and manipulate SQL servers. SQL is a scripting language that is interpreted by the database server. SQL is used to...

- Define database structure
- Manipulate stored data
- Define data access permissions
- Control concurrent data access
- Query stored data

To accommodate the operations of the above categories, SQL is broken into five sublanguages.

| Sublanguage | Description                                                                 |
| ----------- | --------------------------------------------------------------------------- |
| DDL         | Data Definition Language. Defines data structure                            |
| DML         | Data Manipulation Language. Inserts, Updates, Deletes records               |
| DCL         | Data Control Language. Grants or revokes access permissions to database objects |
| TCL         | Transaction Control Language. Defines concurrent operation boundaries        |
| DQL         | Data Query Language. Searches, filters, groups, and aggregates stored data   |

Each sublanguage is responsible for a specific set of operations and has a specific set of commands associated with them. Breaking down each sublanguage is beyond the scope of this document, but they will be discussed in more depth in their own sections.

SQL itself is generally case-insensitive, but it's a good practice to follow a consistent naming convention (e.g., always using lowercase or uppercase) for tables, columns, and other identifiers to avoid potential issues related to case sensitivity.

</details>
<details><summary>Real World Application</summary>
<br>

SQL is used to administer SQL-based RDBMS systems. Below is a short list of some databases and their enterprise users.

- Oracle
  - Wells Fargo
  - Verizon
  - Citi
  - ADP
  - FEMA
- MySQL
  - WordPress
  - NASA
  - Netflix
  - YouTube
  - Bank of America
- PostgreSQL
  - Twitch
  - Apple
  - Spotify
  - Reddit
  - IMDb
- Microsoft SQL Server
  - Fisher Investments
  - Penske
  - Alarm.com
  - Citi
  - Humana
- MariaDB
  - Moodle
  - Samsung
  - Nokia
  - Red Hat
  - SelectQuote
  - Walgreens

</details>
<details><summary>Implementation</summary> 
<br>

SQL is developed based on the [ANSI SQL Standard](https://www.itl.nist.gov/div897/ctg/dm/sql_info.html). However, there are a lot of different vendor-specific implementations available. Below is a list of popular, but not exhaustive, SQL implementations.

- [Oracle](https://docs.oracle.com/en/database/oracle/oracle-database/)
- [MySQL](https://dev.mysql.com/doc/)
- [PostgreSQL](https://www.postgresql.org/docs/)
- [Microsoft SQL Server](https://docs.microsoft.com/en-us/sql/sql-server/?view=sql-server-ver16)
- [MariaDB](https://mariadb.com/kb/en/documentation/)
- [SQLite](https://www.sqlite.org/docs.html)

</details>
<details><summary>Summary</summary> 
<br>

Structured Query Language is the language used to administer SQL-based RDBMS systems. SQL is based on the ANSI standard `ISO/IEC 9075:2016 (ANSI X3.135)`. There are many vendor-specific implementations of the SQL standard, but the standard itself can be divided into five sublanguage categories: `DDL`, `DML`, `DCL`, `TCL`, `DQL`. Each sublanguage is responsible for a specific set of operations on the database.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
