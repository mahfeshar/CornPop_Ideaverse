---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---

-  لما بتعمل login لل MySQL بالطريقة العادية وتكتب الباسوورد ال current database اللي بتبقا متحدده بتبقا NULL
- Log in
```sh
mysql -u root -p
Enter password:
```
- To display the current database:
```sh
SELECT database();

+------------+
| database() |
+------------+
| NULL       |
+------------+
1 row in set (0.00 sec)
```
- It means the current database is not set. If you issue a statement, MySQL will issue an error.
```sql
SELECT * FROM t;

ERROR 1046 (3D000): No database selected
```
- To select a database to work with:
```sql
USE database_name;

Database changed
```
- We can select database when we login
you can use the `-D`
```sh
mysql -u root -D classicmodels -p
```