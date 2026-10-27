 <br>

Consider any database, for example, an Office Database with Employee, Branch, and Client tables. Employee table will have a foreign key called branch_id which is the primary key for the Branch table and the Client table will have a foreign key called employee_id which is a Primary key for Employee table. Any changes made in the Branch table will affect the Employee table. If a branch is closed (deleted), all the employees in that branch are fired (deleted), and if an employee leaves the company(deleted), all the clients of the employee in the Client table are lost (deleted).
