---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
---
- In MySQL, a primary key is a column or a set of columns that uniquely identifies each row in the table. A primary key column must contain unique values.
- If the primary key consists of multiple columns, the combination of values in these columns must be unique. Additionally, a primary key column cannot contain NULL.
- A table can have either zero or one primary key, but not more than one.

### Defining a single-column primary key
You define it for a table when you [[Create Tables]].
```sql
CREATE TABLE table_name(
	column1 datatype PRIMARY KEY,
	column2 datatype,
	...
);
```
In this syntax, you define the `PRIMARY KEY` constraint as a _column constraint_.

Additionally, you can put the `PRIMARY KEY` at the end of the column list:
```sql
CREATE TABLE table_name(
	column1 datatype,
	column2 datatype,
	...,
	PRIMARY KEY(column1)
);
```
In this syntax, you define the `PRIMARY KEY` constraint as a _table constraint_.
### Defining a multi-column primary key
If the primary key consists of two or more columns, you need to use __a table constraint__ to define the primary key:
```sql
CREATE TABLE table_name(
   column1 datatype,
   column2 datatype,
   column3 datatype,
   ...,
   PRIMARY KEY(column1, column2)
);
```
### Adding a primary key to an existing table
We will use [[ALTER]]
```sql
ALTER TABLE table_name
ADD PRIMARY KEY(column1, column2, ...);
```
### Removing a primary key
We will use [[DROP]]
```sql
ALTER TABLE table_name
DROP PRIMARY KEY;
```