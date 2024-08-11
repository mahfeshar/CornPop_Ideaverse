---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
Link: https://www.mysqltutorial.org/mysql-basics/mysql-order-by/
---
We use it with [[SELECT FROM]]
To sort the rows in the result set, we add `ORDER BY` clause to the `SELECT`
```sql
SELECT
	select_list
FROM
	table_name
ORDER BY
	column1 [ASC|DESC],
	column2 [ASC|DESC],
	...;
```
In this syntax, you specify the one or more columns that you want to sort after the `ORDER BY` clause.

- The `ASC` stands for ascending and the `DESC` stands for descending. 

- By default, the `ORDER BY` clause uses `ASC` if you don’t explicitly specify any option.

- If you want to sort the result set by multiple columns, you specify a comma-separated list of columns in the `ORDER BY` clause.

- When executing the `SELECT` statement with an `ORDER BY` clause, MySQL always evaluates the `ORDER BY` clause after the `FROM` and `SELECT` clauses:

![[Pasted image 20240521163346.png]]
