---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
---

A `NOT NULL` constraint ensures that values stored in a column are not [NULL](https://www.mysqltutorial.org/mysql-basics/mysql-null/). 
```sql
column_name data_type NOT NULL;
```

A column may have only one `NOT NULL` constraint, which enforces the rule that the column must not contain any NULL values.

```sql
CREATE TABLE tasks (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    start_date DATE NOT NULL,
    end_date DATE
);
```

To know the structure of table Description:
```sql
DESC table_name;
```
```sql
+------------+--------------+------+-----+---------+----------------+
| Field      | Type         | Null | Key | Default | Extra          |
+------------+--------------+------+-----+---------+----------------+
| id         | int          | NO   | PRI | NULL    | auto_increment |
| title      | varchar(255) | NO   |     | NULL    |                |
| start_date | date         | NO   |     | NULL    |                |
| end_date   | date         | YES  |     | NULL    |                |
+------------+--------------+------+-----+---------+----------------+
4 rows in set (0.01 sec)
```

It’s a good practice to have the `NOT NULL` constraint in every column of a table unless you have a specific reason not to.

Generally, `NULL` values may complicate your queries because you need to use NULL-related functions such as [ISNULL()](https://www.mysqltutorial.org/mysql-comparison-functions/mysql-isnull-function/), [IFNULL()](https://www.mysqltutorial.org/mysql-control-flow-functions/mysql-ifnull/), and [NULLIF()](https://www.mysqltutorial.org/mysql-control-flow-functions/mysql-nullif/) to handle them.

## Adding a NOT NULL constraint to an existing column
You use the following steps:

1. First, check the current values of the column if there are any `NULL` values.
2. Second, update the `NULL` to non-`NULL`.
3. Third, modify the column with a `NOT NULL` constraint.

```sql
INSERT INTO tasks(title ,start_date, end_date)
VALUES('Learn MySQL NOT NULL constraint', '2017-02-01','2017-02-02'),
      ('Check and update NOT NULL constraint to your database', '2017-02-01',NULL);
```
Second, find rows with `NULLs` in the column `end_date` using the [IS NULL](https://www.mysqltutorial.org/mysql-basics/mysql-is-null/) operator:
```sql
SELECT * FROM tasks 
WHERE end_date IS NULL;
```
Third, [[UPDATE]] the `NULL` values to non-null values. In this case, you can create a rule that sets to one week after the start date when the `end_date` is NULL.

```sql
UPDATE tasks 
SET 
    end_date = start_date + 7
WHERE
    end_date IS NULL;
```

Third, add a `NOT NULL` constraint to the `end_date` column using the following [[ALTER]] statement:
```sql
ALTER TABLE table_name
CHANGE
	old_column_name
	new_column_name column_definition;

ALTER TABLE tasks 
CHANGE 
    end_date 
    end_date DATE NOT NULL;
```

## Removing a NOT NULL constraint
To drop a `NOT NULL` constraint for a column, you use the `ALTER TABLE..MODIFY` statement: [[ALTER]]
```sql
ALTER TABLE table_name
MODIFY column_name column_definition;

-- without the `NOT NULL` constraint.

ALTER TABLE tasks 
MODIFY end_date DATE;
```
## Summary

- Use `NOT NULL` constraint to ensure that a column does not contain any `NULL` values.
- Use `ALTER TABLE ... CHANGE` statement to add a `NOT NULL` constraint to an existing column.
- Use `ALTER TABLE ... MODIFY` to drop a `NOT NULL` constraint from a column.
