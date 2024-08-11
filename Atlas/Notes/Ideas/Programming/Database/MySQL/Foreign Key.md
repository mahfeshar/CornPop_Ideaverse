---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
Link: https://www.mysqltutorial.org/mysql-basics/mysql-foreign-key/
---


- A foreign key is a column or group of columns in a table that links to a column or group of columns in another table. 
- The foreign key places constraints on data in the related tables, which allows MySQL to maintain referential integrity.
- Typically, the foreign key columns of the child table often refer to the [[Primary Key]] columns of the parent table.
- A table can have more than one foreign key where each foreign key references a primary key of the different parent tables.
- A table can have more than one foreign key where each foreign key references a primary key of the different parent tables.

### Syntax
```sql
[CONSTRAINT constraint_name]
FOREIGN KEY [foreign_key_name] (column_name, ...)
REFERENCES parent_table(colunm_name,...)
[ON DELETE reference_option]
[ON UPDATE reference_option]
```

In this syntax:

- First, specify the name of the foreign key constraint that you want to create after the `CONSTRAINT` keyword. If you omit the constraint name, MySQL automatically generates a name for the foreign key constraint.

- Second, specify a list of comma-separated foreign key columns after the `FOREIGN KEY` keywords. The foreign key name is also optional and is generated automatically if you skip it.

- Third, specify the parent table followed by a list of comma-separated columns to which the foreign key columns reference.

- Finally, specify how the foreign key maintains the referential integrity between the child and parent tables by using the `ON DELETE` and `ON UPDATE` clauses. The `reference_option` determines the action that MySQL will take when values in the parent key columns are deleted (`ON DELETE`) or updated (`ON UPDATE`).

MySQL has five reference options: `CASCADE`, `SET NULL`, `NO ACTION`, `RESTRICT`, and `SET DEFAULT`.

- `CASCADE`: if a row from the parent table is deleted or updated, the values of the matching rows in the child table are automatically deleted or updated.
- `SET NULL`:  if a row from the parent table is deleted or updated, the values of the foreign key column (or columns) in the child table are set to `NULL`.
- `RESTRICT`:  if a row from the parent table has a matching row in the child table, MySQL rejects deleting or updating rows in the parent table.
- `NO ACTION`: is the same as `RESTRICT`.
- `SET DEFAULT`: is recognized by the MySQL parser. However, this action is rejected by both InnoDB and NDB tables.

MySQL fully supports three actions: `RESTRICT`, `CASCADE` and `SET NULL`.

If you don’t specify the `ON DELETE` and `ON UPDATE` clause, the default action is `RESTRICT`.
### Example
```sql
CREATE TABLE categories(
  categoryId INT AUTO_INCREMENT PRIMARY KEY, 
  categoryName VARCHAR(100) NOT NULL
) ENGINE = INNODB;
CREATE TABLE products(
  productId INT AUTO_INCREMENT PRIMARY KEY, 
  productName VARCHAR(100) NOT NULL, 
  categoryId INT, 
  CONSTRAINT fk_category FOREIGN KEY (categoryId) 
                         REFERENCES categories(categoryId)
) ENGINE = INNODB;
```