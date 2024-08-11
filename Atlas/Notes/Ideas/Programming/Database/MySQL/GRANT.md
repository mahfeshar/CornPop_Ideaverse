---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
---

- The [[CREATE USER]] statement creates a user account with no privileges امتيازات
- It means that the user account can log in to the MySQL Server, but cannot do anything such as [[SELECT a Database]] and [[MySQL MOC#Querying Data|querying data]] from tables.
- To enable the user account to work with database objects, you need to grant it privileges. You use the `GRANT` statement to assign one or more privileges to the user account.
```sql
GRANT privilege [,privilege],..
ON privilege_level (database.table)
To account_name
WITH GRANT OPTION;
```

In this syntax:

- First, specify one or more privileges after the `GRANT` keyword. If you grant multiple privileges, you need to separate privileges by commas.
- Second, specify the `privilege_level`, which determines the extent to which the privileges apply. More information on privilege levels will be provided shortly.
- Third, specify the account name of the user you want to grant privileges after the `TO` keyword.
- This statement also includes `WITH GRANT OPTION`. This will allow your MySQL user to grant any permissions that it has to other users on the system.

>[!Note]
>Many guides suggest running the `FLUSH PRIVILEGES` command immediately after a `CREATE USER` or `GRANT` statement in order to reload the grant tables to ensure that the new privileges are put into effect:

---
To show the privileges assigned to user:
```sql
SHOW GRANTS FOR super@localhost;
```
## MySQL privilege levels
![[Pasted image 20240522085458.png]]
### Global Privileges

**Global privileges** apply to all databases in a MySQL Server. To assign all global privileges, you use the `*.*` syntax, for example:

```sql
GRANT SELECT 
ON *.* 
TO bob@localhost;
```

The account user `bob@localhost` can manage all databases of the current MySQL Server.

### Database privileges

**Database privileges** apply to all objects in a particular database. To assign database-level privileges, you use the `ON database_name.*` syntax, for example:

```sql
GRANT INSERT 
ON classicmodels.* 
TO bob@localhost;
```

In this example, `bob@localhost` can manage all objects in the `classicmodels` database.

### Table privileges

**Table privileges** apply to all columns in a table. To assign table-level privileges, you use the `ON database_name.table_name` syntax. For example:

```sql
GRANT DELETE 
ON classicmodels.employees 
TO bob@localhsot;
```

In this example, `bob@localhost` can manage rows from the `employees` table in the `classicmodels` database.

If you skip the database name, MySQL uses the default database or issues an error if there is no default database.

### Column privileges

**Column privileges** apply to individual columns within a table. You must specify the column or columns for each privilege. For example:

```sql
GRANT 
   SELECT (employeeNumner,lastName, firstName,email), 
   UPDATE(lastName) 
ON employees 
TO bob@localhost;
```

In this example, `bob@localhost` can select data from four columns:

- `employeeNumber`
- `lastName`
- `firstName`
- `email`

And updates only the `lastName` column in the `employees` table.

### Stored routine privileges

**Stored routine privileges** apply to stored procedures and stored functions. For example:

```sql
GRANT EXECUTE 
ON PROCEDURE CheckCredit 
TO bob@localhost;
```

In this example, `bob@localhost` can execute the stored procedure `CheckCredit` in the current database.
### Proxy user privileges

**Proxy user privileges** allow one user to be a proxy for another. The proxy user gets all the privileges of the proxied user. For example:

```sql
GRANT PROXY 
ON root 
TO alice@localhost;
```

In this example, `alice@localhost` assumes all privileges of the user `root`.
## Permissible privileges for the GRANT statement

| **Privilege**           | **Meaning**                                                                                                                                         | **Level** |            |                    |           |     |     |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | ---------- | ------------------ | --------- | --- | --- |
| **Global**              | **Database**                                                                                                                                        | **Table** | **Column** | **Stored Routine** | **Proxy** |     |     |
| ALL [PRIVILEGES]        | Allow the user to alter and drop stored procedures or stored functions.                                                                             |           |            |                    |           |     |     |
| ALTER                   | Allow the user to use the [ALTER TABLE](https://www.mysqltutorial.org/mysql-basics/mysql-alter-table/) statement                                    | X         | X          | X                  |           |     |     |
| ALTER ROUTINE           | Allow the user to create databases and tables                                                                                                       | X         | X          |                    |           | X   |     |
| CREATE                  | Allow the user to create stored procedures and stored functions                                                                                     | X         | X          | X                  |           |     |     |
| CREATE ROUTINE          | Allow the user to create a temporary table by using `CREATE TEMPORARY TABLE` statement                                                              | X         | X          |                    |           |     |     |
| CREATE TABLESPACE       | Allow the user to create, alter, or drop tablespaces and log file groups                                                                            | X         |            |                    |           |     |     |
| CREATE TEMPORARY TABLES | Allow the user to use the `CREATE USER, DROP USER, RENAME USER`, and `REVOKE ALL PRIVILEGES` statements.                                            | X         | X          |                    |           |     |     |
| CREATE USER             | Allow the user to create or modify the view.                                                                                                        | X         |            |                    |           |     |     |
| CREATE VIEW             | Allow the user to use `DELETE` statement                                                                                                            | X         | X          | X                  |           |     |     |
| DELETE                  | Allow the user to execute stored routines                                                                                                           | X         | X          | X                  |           |     |     |
| DROP                    | Allow the user to drop database, table, and view                                                                                                    | X         | X          | X                  |           |     |     |
| EVENT                   | Allow the user to use events for the Event Scheduler.                                                                                               | X         | X          |                    |           |     |     |
| EXECUTE                 | Allow the user to drop the database, table, and view                                                                                                | X         | X          | X                  |           |     |     |
| FILE                    | Allow the user to have privileges to grant or revoke privileges from other accounts.                                                                | X         |            |                    |           |     |     |
| GRANT OPTION            | Allow the user to create or drop indexes.                                                                                                           | X         | X          | X                  |           | X   | X   |
| INDEX                   | Allow the user to create or drop indexes.                                                                                                           | X         | X          | X                  |           |     |     |
| INSERT                  | Allow the user to use the `INSERT` statement                                                                                                        | X         | X          | X                  | X         |     |     |
| LOCK TABLES             | Allow the user to query to see where the master or slave servers are                                                                                | X         | X          |                    |           |     |     |
| PROCESS                 | Allow the user to see all processes with `SHOW PROCESSLIST` statement.                                                                              | X         |            |                    |           |     |     |
| PROXY                   | Enable user proxying.                                                                                                                               |           |            |                    |           |     |     |
| REFERENCES              | Allow user to create a foreign key                                                                                                                  | X         | X          | X                  | X         |     |     |
| RELOAD                  | Allow the user to use `FLUSH` statement                                                                                                             | X         |            |                    |           |     |     |
| REPLICATION CLIENT      | Allow the user to query to see where master or slave servers are                                                                                    | X         |            |                    |           |     |     |
| REPLICATION SLAVE       | Allow the user to use replicate slaves to read binary log events from the master.                                                                   | X         |            |                    |           |     |     |
| SELECT                  | Allow the user to use `SELECT` statement                                                                                                            | X         | X          | X                  | X         |     |     |
| SHOW DATABASES          | Allow user to show all databases                                                                                                                    | X         |            |                    |           |     |     |
| SHOW VIEW               | Allow the user to use `SHOW CREATE VIEW` statement                                                                                                  | X         | X          | X                  |           |     |     |
| SHUTDOWN                | Allow user to use mysqladmin shutdown command                                                                                                       | X         |            |                    |           |     |     |
| SUPER                   | Allow the user to use other administrative operations such as `CHANGE MASTER TO`, `KILL`, `PURGE BINARY LOGS`, `SET GLOBAL`, and mysqladmin command | X         |            |                    |           |     |     |
| TRIGGER                 | Allow the user to use `TRIGGER` operations.                                                                                                         | X         | X          | X                  |           |     |     |
| UPDATE                  | Allow the user to use the `UPDATE` statement                                                                                                        | X         | X          | X                  | X         |     |     |
| USAGE                   | Equivalent to “no privileges”                                                                                                                       |           |            |                    |           |     |     |