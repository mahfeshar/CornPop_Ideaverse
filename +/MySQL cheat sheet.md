---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---


| Command                              | Output                                                 |
| ------------------------------------ | ------------------------------------------------------ |
| **Getting start**                    |                                                        |
| Install it                           | [[Install MySQL on Ubuntu]]                            |
| `sudo -u root -p`                    | Start it                                               |
| `SHOW DATABASES;`                    | To display all databases                               |
|                                      |                                                        |
| **Managing Databases**               |                                                        |
| `SELECT database();`                 | - Show the current database<br>- By default, it's null |
| `USE database_name;`                 | To select database to work with                        |
| `mysql -u root -D database_name -p`  | To select database when you login                      |
|                                      |                                                        |
| `CREATE DATABASE database_name`      | To create new database                                 |
| `SHOW CREATE DATABASE database_name` | Review the created database                            |
