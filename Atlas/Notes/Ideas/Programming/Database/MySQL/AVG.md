---
up:
  - "[[MySQL MOC]]"
related: 
created: 2024-05-21
Link: https://www.mysqltutorial.org/mysql-aggregate-functions/mysql-avg/
---
- It allows you to calculate the average value of a set of values.
```sql
AVG(DISTINCT expression)
```

You use the [[DISTINCT]] operator in the `AVG` function to calculate the average value of the distinct values.

For example, if you have a set of values 1,1,2,3, the `AVG` function with `DISTINCT` operator will return 2 i.e., `(1 + 2 + 3) / 3`.

## Example
![[Pasted image 20240521172828.png]]

```sql
SELECT
	AVG(buyprice) 'Average Price'
FROM
	products;
```

![[Pasted image 20240521172907.png]]