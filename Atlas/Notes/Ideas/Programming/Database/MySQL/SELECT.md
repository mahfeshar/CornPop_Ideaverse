---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---
## SELECT
We will learn how to use `SELECT` without referencing any table.

Typically, you use a `SELECT` statement to select data from a table in the database:
```sql
SELECT select_list
FROM table_name;
```
In MySQL, the `SELECT` statement doesn’t require the `FROM` clause. It means that you can have a `SELECT` statement without the `FROM` clause like this:
```sql
SELECT select_list;
```
The following example uses the `SELECT` statement to perform a simple calculation:
```sql
SELECT 1 + 1;

+-------+
| 1 + 1 |
+-------+
|     2 |
+-------+
1 row in set (0.00 sec)    
```
MySQL has many built-in functions like [string functions](https://www.mysqltutorial.org/mysql-string-functions/), [date functions](https://www.mysqltutorial.org/mysql-date-functions/), and [math functions](https://www.mysqltutorial.org/mysql-math-functions/). You can use the `SELECT` statement to execute one of these functions.


For example, the following statement uses the NOW() function in the SELECT statement to return the current date and time of the server where MySQL server is running:
```sql
SELECT NOW();

+---------------------+
| NOW()               |
+---------------------+
| 2021-07-26 08:08:02 |
+---------------------+
1 row in set (0.00 sec)
```


If a function has parameters, you need to pass arguments into it. For example, to concatenate multiple strings into a single string, you can use the [CONCAT()](https://www.mysqltutorial.org/mysql-string-functions/mysql-concat/) function:

```sql
SELECT CONCAT('John',' ','Doe');

+--------------------------+
| CONCAT('John',' ','Doe') |
+--------------------------+
| John Doe                 |
+--------------------------+
1 row in set (0.00 sec)
```
## Column alias
To change a column name of the result set, you can use a column alias:
```sql
SELECT expression AS colum_alias
-- or
SELECT expression column_alias;
-- AS is optional
```

Example:
```sql
SELECT CONCAT('corn', ' ', 'Pop') AS name;

+----------+
| name     |
+----------+
| John Doe |
+----------+
1 row in set (0.00 sec)
```