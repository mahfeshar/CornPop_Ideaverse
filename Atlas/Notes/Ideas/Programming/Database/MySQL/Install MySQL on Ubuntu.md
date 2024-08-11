---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
Link: https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04
---
## Installing MySQL
- update the package index on your server if you’ve not done so recently:
```sh
sudo apt update
```
- Then install the `mysql-server` package:

```sh
sudo apt install mysql-server
```
- check version
```sh
mysql --version
mysql  Ver 8.0.36-0ubuntu0.22.04.1 for Linux on x86_64 ((Ubuntu))
```
- Connect to your MySQL server:
```sh
sudo mysql
```
### Enable MySQL service to auto-start on reboot
```sh
sudo systemctl enable mysql.service
```
### Start MySQL Service
```sh
sudo systemctl start mysql.service
```
### Check the status of MySQL Service
```sh
systemctl status mysql.service
```
## Log in to my SQL and change the root's password
- log in 
```sh
sudo mysql
mysql>
```
- change the password
```sql
ALTER USER root@localhost
IDENTIFIED WITH mysql_native_password
BY '<YOUR_PASSWORD>'

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
- exit
```sh
exit
```
- attempt to log in to the MySQL database server with the new password:
```sh
mysql -u root -p
Enter password:
```
- Then go back to using the default authentication method using this command:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```
This will mean that you can once again connect to MySQL as your **root** user using the `sudo mysql` command.
## Configuring MySQL
- Before this step you should make last step to add password without it, it will give you error.
- To configure it
```sh
sudo mysql_secure_installation
```
- It’ll prompt you to enter the root’s password. After you enter the password correctly, you will be asked a series of questions. Press ‘Y’ or ‘N’ for the various security questions.
## Adjusting Password Policy (Not Recommended)
[MySQL, 8.4.3 The Password Validation Component](https://dev.mysql.com/doc/refman/8.0/en/validate-password.html)
We can change the password variables
```sql
SHOW VARIABLES LIKE 'validate_password%';
```

```sql
+--------------------------------------+-------+
| Variable_name                        | Value |
+--------------------------------------+-------+
| validate_password.check_user_name    | ON    |
| validate_password.dictionary_file    |       |
| validate_password.length             | 6     |
| validate_password.mixed_case_count   | 1     |
| validate_password.number_count       | 1     |
| validate_password.policy             | LOW   |
| validate_password.special_char_count | 1     |
+--------------------------------------+-------+
```
then you can set the password policy level lower, for example:

```sql
SET GLOBAL validate_password.length = 6;
SET GLOBAL validate_password.number_count = 0;
```

- لو مش عايزه يطلب باسوورد خلي قيمة ال length بصفر
- بس قيمتها بتبقا
```sql
validate_password.number_count + 
validate_password.special_char_count + 
(2 * validate_password.mixed_case_count)
```

## Connect to server
- To connect:
```sh
mysql -u root -p
```
`-u root` means that you connect to the MySQL Server using the user `root`.
`-p` instructs mysql to prompt for a password.

- To display available databases in the current server:
```sh
SHOW DATABASES;
```

```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.01 sec)
```

## Uninstall
First make sure that MySQL service is stopped.
```sh
sudo systemctl stop mysql
```

Remove MySQL related all packages completely.
```sh
sudo apt-get purge mysql-server mysql-client mysql-common mysql-server-core-* mysql-client-core-*
```
Remove MySQL configuration and data. If you have changed database location in your MySQL configuration, you need to replace `/var/lib/mysql` according to it.

```sh
sudo rm -rf /etc/mysql /var/lib/mysql
```

(Optional) Remove unnecessary packages.

```sh
sudo apt autoremove
```

(Optional) Remove apt cache.

```sh
sudo apt autoclean
```
