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
### Summary

| ERD Element               | Mapping Rule                                   |
|---------------------------|------------------------------------------------|
| **Entities**              | Create a table with primary keys for each entity. |
| **Relationships**         | Use foreign keys to represent relationships.     |
| **1:1 Relationships**     | Merge entities or add a foreign key in one table. |
| **1:N Relationships**     | Place a foreign key in the "many" table.         |
| **M:N Relationships**     | Create a join table with foreign keys from both entities. |
| **Weak Entities**         | Create a table with a composite key (including a foreign key). |
| **Multivalued Attributes**| Use a separate table with a foreign key to the main entity. |
| **Derived Attributes**    | Exclude; calculate as needed.                    |

This table covers the main rules for ERD-to-database mapping.
### 1. Mapping of regular(Strong) Entity Types
![[Pasted image 20241108070613.png]]
### 2. Mapping of Multivalued Attributes
![[Pasted image 20241108070927.png]]
### 3. Mapping Relationships
#### Binary M:N Relationship
![[Pasted image 20241108071618.png]]
![[Pasted image 20241108071628.png]]
#### Binary 1:M Relationship
##### Approach 1
![[Pasted image 20241108071702.png]]![[Pasted image 20241108071715.png]]
##### Approach 2
![[Pasted image 20241108071739.png]]
![[Pasted image 20241108071802.png]]
#### Binary 1:1 Relationship
##### Approach 1 (Total-partial or partial-partial)
![[Pasted image 20241108071822.png]]![[Pasted image 20241108071839.png]]
##### Approach 2 (Total-total)
![[Pasted image 20241108071915.png]]
##### Approach 3 (Partial-partial)
![[Pasted image 20241108072029.png]]
![[Pasted image 20241108072042.png]]
#### Summary
![[Pasted image 20241108072110.png]]
![[Pasted image 20241108072124.png]]