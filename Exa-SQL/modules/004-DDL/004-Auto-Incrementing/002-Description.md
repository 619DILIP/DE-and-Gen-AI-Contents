<br>

* `AUTO INCREMENT` allows a unique number to be generated automatically when a new row is inserted into a table.
* `SERIAL`  is used to create an auto-incrementing integer column.
* Most often, `AUTO INCREMENT` or `SERIAL` acts as a primary key field that we would like to be created automatically every time a new record is inserted.
* Depending on the dialect of SQL you are using will determine if you use the `AUTO INCREMENT` keyword or `SERIAL` keyword. 
    * The syntax for auto-incrementing columns varies among SQL dialects, with differences in implementation. While the concepts are the same, different database systems may use distinct keywords or mechanisms for achieving similar functionality. It is important to refer to the documentation of the specific database system you are working with to understand the correct syntax for auto-incrementing columns.
      * **PostgreSQL** - `SERIAL` implicitly creates a sequence to generate unique values.
      * **MySQL** - `AUTO_INCREMENT` automatically increments the value for each new row.
      * **SQLite** - `AUTOINCREMENT` ensures that each new row inserted into the table will automatically receive a unique and incrementing value.
