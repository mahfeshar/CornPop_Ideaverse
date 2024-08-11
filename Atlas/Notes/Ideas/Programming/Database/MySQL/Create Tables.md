---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
Link: https://www.mysqltutorial.org/mysql-basics/mysql-create-table/
---
The `CREATE TABLE` statement allows you to create a new table in a database.

```sql
CREATE TABLE [IF NOT EXISTS] table_name(
	column1 datatype constraints,
	column2 datatype constraints,
	...
) ENGINE=storage_engine
```

In this syntax:

- `table_name`: This is the name of the table that you want to create.
- `column1`, `column2`, etc.: The names of the columns in the table.
- `datatype`: the data of each column such as `INT`, `VARCHAR`, `DATE`, etc.
- `constraints`: These are optional constraints such as `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, and `FOREIGN KEY`.

> If you create a table with a name that already exists in the database, you’ll get an error. To avoid the error, you can use the `IF NOT EXISTS` option.

- In MySQL, each table has a [storage engine](https://www.mysqltutorial.org/mysql-administration/mysql-storage-engines/) such as InnoDB or MyISAM. The `ENGINE` clause allows you to specify the storage engine of the table.
- If you don’t explicitly specify a storage engine, MySQL will use the default storage engine which is InnoDB.

### Example
```sql
CREATE TABLE tasks (
    `id` INT PRIMARY KEY,
    `title` VARCHAR(255) NOT NULL,
    `start_date` DATE,
    `due_date` DATE
);
```
--- 
To list all tables: [[Show Tables]]