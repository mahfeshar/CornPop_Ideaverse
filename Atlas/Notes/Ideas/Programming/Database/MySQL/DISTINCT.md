---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---
To remove these duplicate rows, you use the `DISTINCT` clause in the 
[[SELECT FROM]] statement.
```sql
SELECT DISTINCT
    select_list
FROM
    table_name
WHERE 
    search_condition
ORDER BY 
    sort_expression;
```

![[Pasted image 20240521173618.png]]

When you specify a column that has [NULL](https://www.mysqltutorial.org/mysql-basics/mysql-null/) values in the `DISTINCT` clause, the `DISTINCT` clause will keep only one `NULL` value because it considers all `NULL` values are the same.