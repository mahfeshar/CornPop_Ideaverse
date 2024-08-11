---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
---

- You use the `AUTO_INCREMENT` attribute to automatically generate unique integer values for a column whenever you insert a new row into the table.
- You use the `AUTO_INCREMENT` attribute for the [[Primary Key]] column to ensure each row has a unique identifier.
### Creating a table with MySQL AUTO_INCREMENT column
```sql
CREATE TABLE table_name(
    id INT AUTO_INCREMENT PRIMARY KEY,
    ...
);
```

```sql
CREATE TABLE contacts(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(320) NOT NULL
);
```

When inserting rows into the table with an `AUTO_INCREMENT` column, you don’t need to specify a value for that column. MySQL will automatically generate the value for you.

### Retrieving the last auto-increment value
```sql
SELECT LAST_INSERT_ID();
```

### Resetting the current auto-increment value
We will use [[ALTER]]
```sql
ALTER TABLE table_name 
AUTO_INCREMENT = value;
```
Note that the `ALTER` `TABLE` statement takes effect only if the `value` that you want to reset to is higher than or equal to the maximum value in the `AUTO_INCREMENT` column of the `table_name`.

### Adding an AUTO_INCREMENT column to an existing table
To add an `AUTO_INCREMENT` to an existing table, you use the [[ALTER]] statement.
```sql
CREATE TABLE subscribers(
   email VARCHAR(320) NOT NULL UNIQUE
);

ALTER TABLE subscribers
ADD id INT AUTO_INCREMENT PRIMARY KEY;
```

## Summary

- Assign the `AUTO_INCREMENT` attribute to a column to instruct MySQL to automatically generate unique integer values for the column.