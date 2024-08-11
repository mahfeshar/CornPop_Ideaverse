---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---
- To create a new database, we use the `CREATE DATABASE` statement
```sql
CREATE DATABASE [IF NOT EXISTS] database_name
[CHARACTER SET charset_name]
[COLLATE collation_name];
```
- First, specify the name of the database after the `CREATE DATABASE` keywords. 
  The database name must be unique within a MySQL server instance. 
  If you attempt to create a database with an existing name, MySQL will issue an error.
- Second, use the `IF NOT EXISTS` option to create a database if it doesn’t exist conditionally.
- Third, specify the [character set](https://www.mysqltutorial.org/mysql-basics/mysql-character-set/) and [collation](https://www.mysqltutorial.org/mysql-basics/mysql-collation/) for the new database. 
  If you skip the `CHARACTER SET` and `COLLATE` clauses, MySQL will use the default character set and collation for the new database.

>[!Note]
>write the database name like that \`database_name\`


---
- Review the created database: ^bf0f8b
```sql
SHOW CREATE DATABASE testdb
```
MySQL returns the database name and the character set and collation of the database:
![[Pasted image 20240521122938.png]]