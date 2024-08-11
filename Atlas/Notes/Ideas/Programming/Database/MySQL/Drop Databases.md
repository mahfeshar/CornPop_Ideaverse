---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---
The `DROP DATABASE` statement drops all tables in the database and deletes the database permanently.
```sql
DROP DATABASE [IF EXIST] database_name;
```
- If you drop a database that does not exist, MySQL will issue an error.
- To prevent an error from occurring if you delete a non-existing database, you can use the `IF EXISTS` option.

The `DROP DATABASE` statement returns the number of tables it deleted.

--- 
In MySQL, the schema is the synonym مرادف for the database
```sql
DROP SCHEMA [IF EXISTS] database_name
-- do the same thing
```