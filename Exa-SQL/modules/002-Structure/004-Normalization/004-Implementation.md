<br>

Let's demonstrate normalizing an unnormalized table. In our example, we have a `zookeepers` table. Zookeepers can be responsible for more than one exhibit, and each exhibit can contain more than one animal for them to take care of, and each exhibit can be taken care of by more than one zookeeper.

## Unnormalized
``` sql
CREATE TABLE zookeepers(
	first_name varchar(100),
	last_name varchar(100),
	exhibit varchar(100),
	animal_type1 varchar(100),
	animal_type2 varchar(100),
	animal_type3 varchar(100),
	salary integer,
	position_title varchar(100)
);
```

This table is unnormalized because it does not have a primary key and some columns are redundant.

## 1NF

```sql

CREATE TABLE zookeepers(
	id integer auto_increment PRIMARY KEY,
	first_name varchar(100),
	last_name varchar(100),
	exhibit varchar(100),
	animal_type varchar(100),
	salary integer,
	position_title varchar(100)
);

```

To put the example in 1NF, we added a PK column as well as removed redundant columns. 

## 2NF

``` sql
CREATE TABLE zookeepers(
	id integer auto_increment PRIMARY KEY,
	first_name varchar(100),
	last_name varchar(100),
	salary integer,
	position_title varchar(100)
);

CREATE TABLE exhibits(
	id integer auto_increment PRIMARY KEY, 
	exhibit_name varchar(100)
);

CREATE TABLE animals(
	id integer auto_increment PRIMARY KEY,
	exhibit_id integer, 
	species varchar(100),
	FOREIGN KEY (exhibit_id) REFERENCES exhibits(id) ON DELETE SET NULL
);

CREATE TABLE zookeepers_exhibits(
	zookeeper_id integer,
	exhibit_id integer,
	FOREIGN KEY (zookeeper_id) REFERENCES zookeepers(id) ON DELETE CASCADE,
	FOREIGN KEY (exhibit_id) REFERENCES exhibits(id) ON DELETE CASCADE,
	PRIMARY KEY (zookeeper_id, exhibit_id)
);
```
In order to move our table to 2NF, we needed to remove any columns that don't fully depend on or describe the key or zookeeper entity. Notice we moved exhibit and animal related columns out of the `zookeepers` table. Because there is a many to many relationship between zookeepers and exhibits, we have a bridge or join table that represents the pairings between the two entities. The `animals` table is created and contains a foreign key that references the exhibit table, since an animal would depend on / live within an exhibit.

## 3NF

```sql
CREATE TABLE zookeepers(
	id integer auto_increment primary key,
	position_title_id integer,
	first_name varchar(100),
	last_name varchar(100),
  	FOREIGN KEY (position_title_id) REFERENCES position_titles(id) ON DELETE SET NULL

);

CREATE TABLE position_titles(
	id integer auto_increment primary key,
	position_title_name varchar(100),
	salary integer
);

```
Lastly, we need to remove a transitive dependency so we can move our `zookeepers` table into 3NF. The two columns `salary` and `position_title` did describe the `zookeeper` entity, however if a change is made to the `position_title` column, for example if they are promoted to a `Level 2 Zookeeper` rather than a `Level 1 Zookeeper`, then a change should also be made to the `salary` column. This violates 3NF, so we would need to move these two columns into their own `position_title` table and have the `zookeepers` table depend on it instead.
