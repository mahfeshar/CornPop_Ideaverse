---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---

The `DELETE` statement allows you to delete rows from a table and returns the number of deleted rows.
```sql
DELETE FROM table_name
WHERE condition;
```
In this syntax:

- First, specify the table from which you delete data after the `FROM` keyword.
- Second, specify a condition to determine which rows to delete in the [[WHERE]] clause.

The `WHERE` clause is optional. If you omit the `WHERE` clause, the `DELETE` statement will delete all rows in the table:
```sql
DELETE FROM table_name;
```

> Note that to delete data from multiple related tables, you use the [DELETE JOIN](https://www.mysqltutorial.org/mysql-basics/mysql-delete-join/) statement.

- When you need to remove all rows from a large table and don’t need to know the exact number of rows deleted, you should use the [TRUNCATE TABLE](https://www.mysqltutorial.org/mysql-basics/mysql-truncate-table/) statement for better performance.

In a table that has a [foreign key](https://www.mysqltutorial.org/mysql-basics/mysql-foreign-key/) constraint, when you delete rows from the parent table, MySQL automatically deletes the rows in the child table if the foreign key uses the [ON DELETE CASCADE](https://www.mysqltutorial.org/mysql-basics/mysql-on-delete-cascade/) option.

---
To delete the first three rows, you can use the `DELETE` statement with the [[OREDER BY]] and [LIMIT](https://www.mysqltutorial.org/mysql-basics/mysql-limit/) clauses:
```sql
DELETE FROM table_table
ORDER BY sort_expression
LIMIT row_count;
```