---
up:
  - "[[Database MOC]]"
related: 
created: 2024-11-07
---
![[Pasted image 20241107220617.png]]
- Now we want to **convert** the conceptual ER schema into **a relational database schema**
- This step is called **Mapping**
- We then express this relational schema using SQL code

![[Pasted image 20241107220747.png]]
## Relational Data Model
![[Pasted image 20241107221041.png]]
![[Pasted image 20241107221055.png]]
![[Pasted image 20241107221108.png]]
![[Pasted image 20241108070227.png]]
![[Pasted image 20241108070353.png]]
## Constraints
We talked about [[Conceptual Design (ERD)#Participation Constraints|Participation Constraints]] In relationships
![[Pasted image 20241108070452.png]]
![[Pasted image 20241108070520.png]]
![[Pasted image 20241108070532.png]]
![[Pasted image 20241108070543.png]]

## ER to Relational Mapping
![[Pasted image 20241107220807.png]]
### Mapping Steps
![[Pasted image 20241108095126.png]]
### **Summary**

| ERD Element / Relationship Type | Approach                                                                                                                                                          |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Strong Entities**                    | Create a table for each entity, with attributes as columns and a primary key for unique identification.                                                           |
| **1-to-1 Partial-Partial**      | 1. Use the primary key of one **table** **as a foreign key in the other**.<br> 2. Create a **new table** with the primary keys of both tables as foreign keys.    |
| **1-to-1 Total-Partial**        | Use the primary key of the partial side as a foreign key in the total side.                                                                                       |
| **1-to-1 Total-Total**          | Merge both tables into a single table, as both sides are mandatory.                                                                                               |
| **1-to-Many**                   | 1. Add the primary key of the "1" side as a foreign key in the "many" side.<br> 2. Create a new table with the primary keys of both tables as foreign keys.       |
| **Many-to-Many**                | Create a new table (join table) with the primary keys of both tables as foreign keys, establishing a many-to-many relationship.                                   |
| **Weak Entities**               | Create a table for the weak entity, including a foreign key from the supporting entity and a composite primary key (using the foreign key and unique attributes). |
| **Multivalued Attributes**      | Use a separate table for each multivalued attribute, with a foreign key linking it back to the main entity’s table. Each value is stored as a new row.            |
| **Derived Attributes**          | Exclude from the database schema; calculate dynamically as needed through queries or views.                                                                       |

### 1. Mapping of regular(Strong) Entity Types
![[Pasted image 20241108094305.png]]
#### 1) Composite Attribute
![[Pasted image 20241108070613.png]]
عشان أظهرها بعملها على حسب الـ **Constraint File** أو كنا قولنا عليه Equations File
	فلازم أكتب فيها حاجة زي Composite انها هتظهر الإسم (Mahmoud Feshar) 
	يعني بكتب المعادلة نفسها أو الـ Equation
#### 2) Multivalued Attributes
الـ Complex Attribute زيها برضو بالظبط
![[Pasted image 20241108070927.png]]
![[4.jpeg]]

#### 3) Mapping of Derived Attributes
بنعمل Ignore للـ Derived ونكتب الأصلية بس
ممكن في البيزنيس يخلينا نعملها Column عادي

![[3.jpeg]]

بنكتب برضو المعادلة بتاعنا في الـ Equations File 
	يعني مثلًا `Age = CurrentDate - DOB`
	لو كل مرة هحسب المعادلة دي وأنا مش معايا Resources فاعملها Column عادي 
	أو لو عايز أعمل مثلًا الأبلكيشن يبقا سريع لأنه مش هعمل العملية دي زي الأبلكيشنز اللايت

![[Pasted image 20241108094000.png]]
لازم تعمل منشن في الـ Equation لو هي معتمدة على داتا من Table تاني
### 2. Mapping of Weak Entity Type
![[Pasted image 20241108094858.png]]
افتكر ان الـ Weak Entity مبيبقاش فيها Primary key وبيبقا فيها **Partial Key** 

![[Pasted image 20241108075450.png]]
![[Pasted image 20241108075459.png]]

### 5. Mapping Relationships
#### 1) Binary M:N Relationship
![[Pasted image 20241108071618.png]]
![[Pasted image 20241108071628.png]]
#### 2) Binary 1:M Relationship
##### Approach 1 (Must)
![[Pasted image 20241108071702.png]]![[Pasted image 20241108071715.png]]
##### Approach 2 (May)
![[Pasted image 20241108071739.png]]
![[Pasted image 20241108071802.png]]
#### 3)Binary 1:1 Relationship
##### Approach 1 (Total-partial)
![[Pasted image 20241108071822.png]]![[Pasted image 20241108071839.png]]
![[Pasted image 20241108095925.png]]
##### Approach 2 (Total-total)
![[Pasted image 20241108095715.png]]
![[Pasted image 20241108071915.png]]
##### Approach 3 (Partial-partial)
![[Pasted image 20241108072029.png]]
![[Pasted image 20241108072042.png]]
#### Summary
![[Pasted image 20241108072110.png]]
![[Pasted image 20241108072124.png]]

### 6. Mapping of N-ary Relationship
![[Pasted image 20241108092752.png]]
![[Pasted image 20241108092804.png]]