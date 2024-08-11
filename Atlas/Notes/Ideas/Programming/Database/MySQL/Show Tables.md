---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
Link: https://www.mysqltutorial.org/mysql-administration/mysql-show-tables/
---
**Syntax**:
```sql
SHOW TABLES;
```
- you should use first the database that you want to show it 

```
+-------------------------+
| Tables_in_classicmodels |
+-------------------------+
| customers               |
| employees               |
| offices                 |
| orderdetails            |
| orders                  |
| payments                |
| productlines            |
| products                |
+-------------------------+
8 rows in set (0.00 sec)
```
---
To include the table type in the result, you use the following form of the `SHOW TABLES` statement.
```sql
SHOW FULL TABLES;
```

```
+-------------------------+------------+
| Tables_in_classicmodels | Table_type |
+-------------------------+------------+
| customers               | BASE TABLE |
| employees               | BASE TABLE |
| offices                 | BASE TABLE |
| orderdetails            | BASE TABLE |
| orders                  | BASE TABLE |
| payments                | BASE TABLE |
| productlines            | BASE TABLE |
| products                | BASE TABLE |
+-------------------------+------------+
8 rows in set (0.00 sec)
```
---
To Show the full description of the table.
```sql
SHOW CREATE `first_table`;
```
We used it before at [[Create Databases#^bf0f8b|Create Databases]]
