---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-22
---
### What is a JOIN in SQL?
JOIN is a clause used in SQL to link data from one table to another table using one or more data column shared between two tables.

In other words, we combine data of the two existing tables into one. For example, **`table1`** has data about `x` and `y`, **`table2`** has data about `y` and `z`, so we join **`table1`** and **`table2`** to get a **`table3`** with all data of `x`, `y`, and `z`.

### How important is JOIN in SQL?
For storing data, it’s not efficient to put everything into one table as it makes the table become heavier and lower its performance a lot. 
So it’s better to divide information into many different tables, faster storing, faster retrieving. But every now and then, you will need to select data from multiple tables, that’s where JOIN comes in handy.

Normally a **`JOIN`** has an **`ON`** condition and depending on the type of JOINs, it will return all the record from one table, or both, if there’s a match with the **`ON`** condition.

### 7 types of JOINs and how to use them

![[Pasted image 20240522203259.png]]
#### **1. INNER JOIN**
- It’s the intersection between two tables.

![[Pasted image 20240522201953.png]]
```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.col1 = table2.col2;
```
#### **2. FULL (OUTER) JOIN**
- returns all the records that match the ON condition, no matter which table they are stored in

![[Pasted image 20240522202104.png]]
```sql
SELECT *
FROM table1
FULL JOIN table2
ON table1.col1 = table2.col2;
```

#### **3. FULL (OUTER) JOIN without the intersection.**
- This clause returns all records that match the ON condition, excluding those are in common between two tables, or those records exist in both tables.

- In plain term, it can be understood as (OUTER JOIN) - (INNER JOIN).

![[Pasted image 20240522202302.png]]
```sql
SELECT *
FROM table1 AS t1
FULL JOIN table2 AS t2
ON t1.col1 = t2.col2
WHERE t1.col1 IS NULL
OR t1.col2 IS NULL;
```

#### **4. LEFT (OUTER) JOIN**
- **`LEFT JOIN`** returns all records from the left table (table1) that matched the ON condition.

![[Pasted image 20240522202447.png]]
```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.col1 = table2.col2;
```
#### **5. LEFT (OUTER) JOIN without the intersection**

- This clause returns all records from the left table (table1) that matched the ON condition, but exclude those are in common better two tables, or those records exist in both tables.

- In plain term, it can be understood as (LEFT JOIN) - (INNER JOIN).

![[Pasted image 20240522202611.png]]
```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.col1 = table2.col2
WHERE table2.col2 IS NULL;
```

#### **6. RIGHT (OUTER) JOIN**
In the opposite of **`LEFT JOIN`**, **`RIGHT JOIN`** returns all records from the right table (table2) that matched the ON condition.

![[Pasted image 20240522202755.png]]
```sql
SELECT *
FROM table1
RIGHT JOIN table2
ON table1.col1 = table2.col2;
```

#### **7. RIGHT (OUTER) JOIN without the intersection**
- This clause returns all records from the right table (table2) that matched the ON condition, but exclude those are in common better two tables, or those records exist in both tables.

- In plain term, it can be understood as (RIGHT JOIN) - (INNER JOIN).

![[Pasted image 20240522202847.png]]
```sql
SELECT *
FROM table1
RIGHT JOIN table2
ON table1.col1 = table2.col2
WHERE table1.col1 IS NULL;
```
