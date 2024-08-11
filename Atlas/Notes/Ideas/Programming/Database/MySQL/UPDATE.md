---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---

The `UPDATE` statement updates data in a table. 
It allows you to change the values in one or more columns of a single row or multiple rows.

```sql
UPDATE [LOW_PRIORITY] [IGNORE] table_name 
SET 
    column_name1 = expr1,
    column_name2 = expr2,
    ...
[WHERE
    condition];
```

In this syntax:

- First, specify the name of the table that you want to update data after the `UPDATE` keyword.
- Second, specify which column you want to update and the new value in the `SET` clause. To update values in multiple columns, you use a list of comma-separated assignments by supplying a value in each column’s assignment in the form of a literal value, an expression, or a [subquery](https://www.mysqltutorial.org/mysql-basics/mysql-subquery/ "MySQL Subquery").
- Third, specify which rows to be updated using a condition in the [[WHERE]] clause. The `WHERE` clause is optional. If you omit it, the `UPDATE` statement will modify all rows in the table.

> [!Note]
> Notice that the `WHERE` clause is so important that you should not forget. Sometimes, you may want to update just one row; However, you may forget the `WHERE` clause and accidentally update all rows of the table.

MySQL supports two modifiers in the `UPDATE` statement.

1. The `LOW_PRIORITY` modifier instructs the `UPDATE` statement to delay the update until there is no connection reading data from the table. The `LOW_PRIORITY` takes effect for the [storage engines](https://www.mysqltutorial.org/mysql-administration/mysql-storage-engines/) that use table-level [locking](https://www.mysqltutorial.org/mysql-basics/mysql-table-locking/) only such as `MyISAM`, `MERGE`, and `MEMORY`.
2. The `IGNORE` modifier enables the `UPDATE` statement to continue updating rows even if errors occurred. The rows that cause errors such as duplicate-key conflicts are not updated.