---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
Link: https://www.mysqltutorial.org/mysql-aggregate-functions/mysql-count/
---

- It returns the number of rows in a table
- The `COUNT()` function allows you to count all rows or only rows that match a specified condition.

The `COUNT()` function has three forms:

- `COUNT(*)`
- `COUNT(expression)`
- `COUNT(DISTINCT expression)`

--- 
### COUNT(\*) function

The `COUNT(*)` function returns the number of rows in a result set returned by a [[SELECT FROM]] statement. 
The `COUNT(*)` returns the number of rows _including duplicate, non-NULL and `NULL` rows_.

### COUNT(expression)

The `COUNT(expression)` returns the number of rows that _do not contain `NULL` values_ as the result of the expression.

### COUNT(DISTINCT expression)

The `COUNT(DISTINCT expression)` returns the number of _distinct rows that do not contain `NULL` values_ as the result of the expression.

The return type of the `COUNT()` function is [BIGINT](https://www.mysqltutorial.org/mysql-basics/mysql-int/). 
The `COUNT()`  function returns 0 if there is no matching row found.

## Example
First, Create table:
```sql
CREATE TABLE count_demos (
	id INT AUTO_INCREMENT PRIMARY KEY,
	val INT
);
```
Second, insert some rows:
```sql
INSERT INTO count_demos(val)
VALUES (1), (1),(2),(2),(NULL),(3),(4),(NULL),(5);
```
Third, query data:
```sql
SELECT * FROM count_demos;
```

![[Pasted image 20240521154548.png]]
### COUNT(\*)
return all rows
```sql
SELECT COUNT(*) FROM count_demos;
```
![[Pasted image 20240521154633.png]]
We can specify a condition to count only what I want with [[WHERE]]
```sql
SELECT COUNT(*)
FROM count_demos
WHERE val = 2;
```
![[Pasted image 20240521154807.png]]
### COUNT(expression)
If you specify the `val` column in the `COUNT()` function, the `COUNT()` function will count only rows with non-NULL values in the `val` column:
```sql
SELECT COUNT(val)
FROM count_demose;
```
![[Pasted image 20240521154854.png]]
Notice that two `NULL` values are not counted.
### COUNT(DISTINCT expression)
This example uses `COUNT(DISTINCT expression)` to count non-NULL and distinct values in the column `val`:
```sql
SELECT COUNT(DISTINCT val)
FROM count_demos;
```
![[Pasted image 20240521155124.png]]