---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---

The `SELECT` statement allows you to select data from one or more tables.
```sql
SELECT select_list
FROM table_name;
```
In this syntax:

- First, specify one or more columns from which you want to select data after the `SELECT` keyword. If the `select_list` has multiple columns, you need to separate them by a comma (`,`).
- Second, specify the name of the table from which you want to select data after the `FROM` keyword.

> [!Note]
> The semicolon (`;`) is optional, which denotes the end of a statement. If you have two or more statements, you need to use the semicolon(`;)` to separate them so that MySQL will execute each statement individually.

When executing the `SELECT` statement, MySQL evaluates the `FROM` clause before the `SELECT` clause:
![[Pasted image 20240521140101.png]]
## Examples
![[Pasted image 20240521140127.png]]
The `employees` table has eight columns: employeeNumber, lastName, firstName, extension, email, officeCode, reportsTo, and jobTitle.

1. retrieve data from a single column
```sql
SELECT lastname
FROM employees;
```
```
+-----------+
| lastName  |
+-----------+
| Murphy    |
| Patterson |
| Firrelli  |
| Patterson |
| Bondur    |
| Bow       |
| Jennings  |
...
```

>[!info]
>The result of a `SELECT` statement is called a **result set** as it’s a set of rows that results from the query.

2. query data from multiple columns
```sql
SELECT 
	lastName,
	firstName,
	jobTitel
FROM
	emplyees;
```
```
+-----------+-----------+----------------------+
| lastname  | firstname | jobtitle             |
+-----------+-----------+----------------------+
| Murphy    | Diane     | President            |
| Patterson | Mary      | VP Sales             |
| Firrelli  | Jeff      | VP Marketing         |
| Patterson | William   | Sales Manager (APAC) |
| Bondur    | Gerard    | Sale Manager (EMEA)  |
...
```

3. retrieve data from all columns
```sql
SELECT employeeNumber,
       lastName,
       firstName,
       extension,
       email,
       officeCode,
       reportsTo,
       jobTitle
FROM   employees; 
```
you can use the asterisk (\*) which is the shorthand for all columns.
```sql
SELECT *
FROM employees;
```

- The `SELECT *` is often called “select star” or “select all” since it selects data from all columns of the table. In practice, you should use the `SELECT *` for the ad-hoc queries only.

- If you embed the `SELECT` statement in the code such as [PHP](https://www.mysqltutorial.org/php-mysql/), [Java](https://www.mysqltutorial.org/mysql-jdbc-tutorial/), [Python](https://www.mysqltutorial.org/python-mysql/), and [Node.js](https://www.mysqltutorial.org/mysql-nodejs/), you should explicitly specify the columns from which you want to select data.