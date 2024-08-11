---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
---

A `UNIQUE` constraint is an integrity constraint that ensures the uniqueness of values in a column or group of columns. A `UNIQUE` constraint can be either a column constraint or a table constraint.

To define a `UNIQUE` constraint for a column when [[Create Tables]], you use the following syntax:
```sql
CREATE TABLE table_name(
    ...,
    column1 datatype UNIQUE,
    ...
);
```
To define a `UNIQUE`  constraint for two or more columns, you use the following syntax:
```sql
CREATE TABLE table_name(
	column1 datatype,
	column2 datatype,
	...,
	UNIQUE(column1, column2)
);
```
If you define a `UNIQUE` constraint without specifying a name, MySQL automatically generates a name for it. To define a `UNIQUE` constraint with a name, you use this syntax:
```sql
[CONSTRAINT constraint_name]
UNIQUE(column_list)
```
In this syntax, you specify the name of the `UNIQUE` constraint after the `CONSTRAINT` keyword.

```sql
CREATE TABLE suppliers (
    supplier_id INT AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    phone VARCHAR(15) NOT NULL UNIQUE,
    address VARCHAR(255) NOT NULL,
    PRIMARY KEY (supplier_id),
    CONSTRAINT uc_name_address UNIQUE (name,address)
);
```
## MySQL UNIQUE constraint & NULL

In MySQL, NULL values are treated as distinct when it comes to unique constraints. Therefore, if you have a column that accepts NULL values, you can insert multiple values into the column.

```sql
CREATE TABLE contacts(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    phone VARCHAR(20) UNIQUE
);

INSERT INTO contacts(name, phone)
VALUES
   ('Alice','(408)-102-2456'),
   ('John', NULL),
   ('Jane', NULL);

-- No ERROR here
```
## Drop a unique constraint

To drop a `UNIQUE` constraint, you can use [[DROP]] or [[ALTER]] statement:
```sql
DROP INDEX index_name ON table_name;

ALTER TABLE table_name
DROP INDEX index_name;
```

```sql
DROP INDEX uc_name_address ON suppliers;
```

## Add new unique constraint
The following `ALTER TABLE ADD CONSTRAINT` adds a unique constraint to a column of an existing table:
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name 
UNIQUE (column_list);
```