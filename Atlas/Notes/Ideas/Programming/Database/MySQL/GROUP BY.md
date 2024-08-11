---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
---

The `GROUP BY` clause groups a set of rows into a set of summary rows based on column values or expressions. 
It returns one row for each group and reduces the number of rows in the result set.

```sql
SELECT 
    c1, c2,..., cn, aggregate_function(ci)
FROM
    table_name
WHERE
    conditions
GROUP BY c1 , c2,...,cn;
```

![[Pasted image 20240521173933.png]]

We use [[MySQL MOC#Aggregate Functions|Aggregate Functions]] with `GROUP BY`