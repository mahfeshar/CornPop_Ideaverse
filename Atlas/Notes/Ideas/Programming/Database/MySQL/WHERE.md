---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---

The `WHERE` clause allows you to specify a search condition for the rows returned by a query.
```sql
SELECT 
    select_list
FROM
    table_name
WHERE
    search_condition;
```
The `search_condition` is a combination of one or more expressions using the logical operator [AND](https://www.mysqltutorial.org/mysql-basics/mysql-and/)`, `[OR](https://www.mysqltutorial.org/mysql-basics/mysql-or/) and `NOT`.

In MySQL, a predicate is a [Boolean](https://www.mysqltutorial.org/mysql-basics/mysql-boolean/) expression that evaluates to `TRUE`, `FALSE`, or `UNKNOWN`.

- The `SELECT` statement will include any row that satisfies the `search_condition` in the result set.

- Besides the `SELECT` statement, you can use the `WHERE` clause in the [[UPDATE]] or [`DELETE`](https://www.mysqltutorial.org/mysql-basics/mysql-delete/) statement to specify which rows to update or delete.

- When executing a [[SELECT FROM]] statement with a `WHERE` clause, MySQL evaluates the `WHERE` clause after the `FROM` clause and before the `SELECT` and `ORDER BY` clauses:

![[Pasted image 20240521170132.png]]
