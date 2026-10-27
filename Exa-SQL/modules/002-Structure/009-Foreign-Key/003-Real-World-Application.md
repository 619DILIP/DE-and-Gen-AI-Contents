<br>

Consider any database, for example, a company database, an `employee` table has details like `id`, `name`, `branch id`, `address`, `manager id`, etc. Consider another table called `branch` which an employee belongs to. `branch id` in the employee table is a foreign key referencing the primary key of the `branch` table.

Similarly, consider another table called `client`, which has details like `client name`, `employee id`, etc. the `employee id` in `client` table is a foreign key referencing the primary key of `employee` table.
