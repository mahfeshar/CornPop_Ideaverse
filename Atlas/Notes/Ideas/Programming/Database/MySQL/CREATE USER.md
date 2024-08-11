---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
---

- MySQL creates the root user account during installation. 
- This root user account has __full privileges__ over the MySQL database server, giving it complete control over all databases, tables, users, and more.
- It’s a good practice to use the root account for administrative functions exclusively.

--- 
To create a new user in the MySQL database, you use the `CREATE USER` statement.
```sql
CREATE USER [IF NOT EXISTS] account_name 
IDENTIFIED BY 'password';
```

In this syntax:

First, specify the account name after the `CREATE USER` keywords. The account name consists of two parts: `username` and `hostname`, separated by the `@` sign:

```sql
username@hostname
```

The `username` is the name of the user while the `hostname` is the name of the host from which the user connects to the MySQL Server.

The `hostname` part of the account name is optional. If you omit the hostname, the user can connect from any host.

An account name without a hostname is equivalent to the following:

```sql
username@%
```

If the `username` and `hostname` contains special characters, such as spaces or hyphens, you need to enclose the username and hostname separately in quotes, like this:

```sql
'bob-cat'@'hostname'
```

In addition to the single quote (`'`), you can use backticks ( `` ` ``) or double quotation mark (`"`).

Second, specify the password for the user after the `IDENTIFIED BY` keywords.

The `IF NOT EXISTS` option creates a new user only if it does not already exist. If the user exists, the statement issues a warning.

>[!Note]
>Note that the `CREATE USER` statement creates a new user without any privileges. To [grant privileges](https://www.mysqltutorial.org/mysql-administration/mysql-grant/) to the user, you use the [[GRANT]] statement.

---
To Show all users:
```sql
SELECT
	user
FROM
	mysql.user;
```
Example:
```sql
create user bob@localhost identified by 'Secure1pass!';
```