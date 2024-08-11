---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
---

It allows you to specify a default value for a column. Here’s the syntax of the `DEFAULT` constraint:
```sql
column_name data_type DEFAULT default_value;
```

- The `default_value` must be a literal constant, e.g., a number or a string. It cannot be a function or an expression. However, MySQL allows you to set the current date and time (`CURRENT_TIMESTAMP`) to the [TIMESTAMP](https://www.mysqltutorial.org/mysql-basics/understanding-mysql-timestamp/) and [DATETIME](https://www.mysqltutorial.org/mysql-basics/mysql-datetime/) columns.

- When you define a column without the [[NOT NULL]] constraint, the column will implicitly take `NULL` as the default value.

- Typically, you set the `DEFAULT` constraints for columns when you [[Create Tables]]

## Example
```sql
CREATE TABLE cart_items 
(
    item_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    quantity INT NOT NULL,
    price DEC(5,2) NOT NULL,
    -- HERE
    sales_tax DEC(5,2) NOT NULL DEFAULT 0.1,
    CHECK(quantity > 0),
    CHECK(sales_tax >= 0) 
);
```

## Adding a DEFAULT constraint to a column
To add a default constraint to a column of an existing table, you use the [[ALTER]] statement:
```sql
ALTER TABLE table_name
ALTER COLUMN column_name SET DEFAULT default_value;

ALTER TABLE cart_items
ALTER COLUMN quantity SET DEFAULT 1;
```
## Removing a DEFAULT constraint from a column
To remove a `DEFAULT` constraint from a column, you use the `ALTER TABLE` statement: [[ALTER]]
```sql
ALTER TABLE table_name
ALTER column_name DROP DEFAULT;

ALTER TABLE cart_items
ALTER COLUMN quantity DROP DEFAULT;
```

## Summary

- MySQL `DEFAULT` constraints set default values for columns.
- Use `DEFAULT default_value` to set a default constraint to a column.
- Use `ALTER TABLE ... ALTER COLUMN ... SET DEFAULT` to add a `DEFAULT` constraint to a column of an existing table.
- Use `ALTER TABLE ... ALTER COLUMN ... DROP DEFAULT` to drop a `DEFAULT` constraint from a column of an existing table.