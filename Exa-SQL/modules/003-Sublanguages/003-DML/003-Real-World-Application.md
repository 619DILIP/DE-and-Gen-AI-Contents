<br>

DML is used to manipulate the data that is being stored in the database. Often DML is used in enterprise application solutions that utilize bridging libraries like JDBC in Java or EF in .NET, but of course it is possible to use DML directly in a SQL IDE or console. In the real world, DBA could be responsible for adding data to bootstrap the database into a working state for the applications that will rely on the data.

Let's bootstrap the permissions and roles tables in the following IAM schema:
```SQL
CREATE DATABASE IF NOT EXISTS IAM;

USE IAM;

CREATE TABLE IF NOT EXISTS permission_categories (
	id BIGINT PRIMARY KEY,
    name VARCHAR(30) NOT NULL UNIQUE,
    description TEXT(255)
);

CREATE TABLE IF NOT EXISTS permissions (
	id BIGINT PRIMARY KEY,
    categoryId BIGINT NOT NULL,
    name VARCHAR(30) NOT NULL UNIQUE,
    index(categoryId, name)
);

CREATE TABLE IF NOT EXISTS roles (
	id BIGINT PRIMARY KEY,
    name VARCHAR(30) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS roles_permissions(
	roleId BIGINT,
    permissionId BIGINT,
    PRIMARY KEY(roleId, permissionId)
);

CREATE TABLE  IF NOT EXISTS login_activities_lu (
	id BIGINT PRIMARY KEY,
    type VARCHAR(10) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS profiles (
	id BIGINT PRIMARY KEY,
    firstName VARCHAR(30) NOT NULL,
    lastName VARCHAR(40) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS users (
	id BIGINT PRIMARY KEY,
    username VARCHAR(20) NOT NULL UNIQUE,
    password VARCHAR(20) NOT NULL,
    profileId BIGINT NOT NULL,
    isActive BOOLEAN DEFAULT true,
    isLocked BOOLEAN DEFAULT false
);

CREATE TABLE IF NOT EXISTS login_activities (
	id BIGINT PRIMARY KEY,
    userId BIGINT NOT NULL,
    activityId BIGINT NOT NULL,
    activityDate DATETIME DEFAULT NOW()
);

CREATE TABLE IF NOT EXISTS users_roles (
	userId BIGINT NOT NULL,
    roleId BIGINT NOT NULL
);

ALTER TABLE permissions ADD CONSTRAINT fk_permissions_category_id FOREIGN KEY(categoryId) REFERENCES permission_categories(id);
ALTER TABLE roles_permissions ADD CONSTRAINT fk_permissions_role_id FOREIGN KEY(roleId) REFERENCES roles(id);
ALTER TABLE roles_permissions ADD CONSTRAINT fk_roles_permission_id FOREIGN KEY(permissionId) REFERENCES permissions(id);
ALTER TABLE users ADD CONSTRAINT fk_users_profile_id FOREIGN KEY(profileId) REFERENCES profiles(id);
ALTER TABLE login_activities ADD CONSTRAINT fk_login_user_id FOREIGN KEY(userId) REFERENCES users(id);
ALTER TABLE login_activities ADD CONSTRAINT fk_login_activity_id FOREIGN KEY(activityId) REFERENCES login_activities_lu(id);
ALTER TABLE users_roles ADD CONSTRAINT fk_ur_user_id FOREIGN KEY(userId) REFERENCES users(id);
ALTER TABLE users_roles ADD CONSTRAINT fk_ur_role_id FOREIGN KEY(roleId) REFERENCES roles(id);
```

We'll use DML's `INSERT INTO` commands to add information or data into our tables.

```SQL
INSERT INTO roles (id, name) values (1, 'ADMIN'), (2, 'OWNER'), (3, 'EDITOR'), (4, 'VIEWER');
INSERT INTO permission_categories (id, name, description) VALUES (1, 'HR', 'Permissions assigned to members of the HR team'),
	(2, 'Accounting', 'Permissions assigned to members of the accounting team'), (3, 'Technology', 'Permissions assigned to members of the technology team');
INSERT INTO permissions (id, categoryId, name) VALUES (1, 1, 'TIMESHEETS'), (2, 2, 'PAYROLL'), (3, 3, 'EVALUATION');
```

The actual amount of bootstrapping that could be done is dependent on the problem at hand, and of course IAM is a very large problem. The above could demonstrates the use of the insert statements of DML in the schema. Pay attention to the order some of the statements. For instance the `permissions` table has a relationship with `permission_catagories` so in order to insert the categoryId into the `permissions` table we must first insert it into the `permission_catagories` table.

Should the need arise to modify a record in the database, like re-assign the 'PAYROLL' permission from 'Accounting' to 'HR'.

```SQL
UPDATE permissions SET categoryId=1;
```

Or should the need arise to remove the 'VIEWER' role.

```SQL
DELETE FROM roles WHERE name='VIEWER';
```
