---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---
The `INSERT` statement allows you to insert one or more rows into a table.
```sql
INSERT INTO table_name(column1, column2, ...)
VALUES (value1, value2, ...);
```

In this syntax,

- First, specify the table name and a list of comma-separated columns inside parentheses after the `INSERT INTO` clause.
- Then, put a comma-separated list of values of the corresponding columns inside the parentheses following the `VALUES` keyword.

>[!hint]
>When using the `INSERT` statement, you need to ensure that the number of columns matches the number of values.

Additionally, you need to specify that the positions of columns correspond precisely to the positions of their corresponding values.


### To insert multiple rows
To insert multiple rows into a table using a single `INSERT` statement, you use the following syntax:
```sql
INSERT INTO table(column1, colum2, ...)
VALUES
	(value1, value2, ...),
	(value1, value2, ...),
	...
	(value1, value2, ...);
```
In this syntax, rows are separated by commas in the `VALUES` clause.
## Examples
Let's create a new table called `tasks`
```sql
DROP TABLE IF EXISTS tasks;

CREATE TABLE tasks (
  task_id INT AUTO_INCREMENT PRIMARY KEY, 
  title VARCHAR(255) NOT NULL, 
  start_date DATE, 
  due_date DATE, 
  priority TINYINT NOT NULL DEFAULT 3, 
  description TEXT
);
```

### 1. Basic MySQL INSERT statement
```sql
INSERT INTO tasks(title, priority)
VALUES('Learn MySQL INSERT Statement', 1);

-- Output: `1 row(s) affected`
```
In this example, we specified values for the `title` and `priority` columns only. For other columns, MySQL uses the default values.

The `task_id` column is an [AUTO_INCREMENT](https://www.mysqltutorial.org/mysql-basics/mysql-auto_increment/) column, meaning that MySQL generates a sequential integer whenever a row is inserted into the table.
### 2. Inserting rows using default value
If you want to insert a default value into a column, you have two ways:

- Ignore both the column name and value in the `INSERT` statement.
- Specify the column name in the `INSERT INTO` clause and use the `DEFAULT` keyword in the `VALUES` clause.
```sql
INSERT INTO tasks(title, priority)
VALUES('Understanding DEFAULT', DEFAULT);
```

Lets list all rows:
```sql
SELECT * FROM tasks;
```

![[Pasted image 20240521141806.png]]
### 3. Inserting dates into the table
To insert a literal date value into a column, you use the following format:

`'YYYY-MM-DD'`Code language: SQL (Structured Query Language) (sql)

In this format:

- `YYYY` represents a four-digit year e.g., 2018.
- `MM` represents a two-digit month e.g., 01, 02, and 12.
- `DD` represents a two-digit day e.g., 01, 02, 30.
```sql
INSERT INTO tasks (title, start_date, due_date)
VALUES ('Insert date into table', '2018-01-09', '2018-09-15');
```
It is possible to use expressions in the `VALUES` clause. For example, the following statement adds a new task using the current date for the start date and due date columns:
```sql
INSERT INTO tasks(title, start_date, due_date) 
VALUES 
  (
    'Use current date for the task', 
    CURRENT_DATE(), 
    CURRENT_DATE()
  );
```
In this example, we used the `CURRENT_DATE()` function as the values for the `start_date` and `due_date` columns. Note that the [CURRENT_DATE()](https://www.mysqltutorial.org/mysql-date-functions/mysql-curdate/) function is a [date function](https://www.mysqltutorial.org/mysql-date-functions/) that returns the current system date.

### 4. Inserting multiple rows
```sql
INSERT INTO tasks(title, priority)
VALUES
	('My first task', 1),
	('It is the second task',2),
	('This is the third task of the week',3);
```
### 5. Dealing with auto-increment column
```sql
INSERT INTO t VALUES();
```
In this statement, we don’t specify any column after the table name and any values inside the VALUES() clause.