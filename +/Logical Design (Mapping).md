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
### **Summary**


| ERD Element / Relationship Type | Approach                                                                                                                                                          |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Entities**                    | Create a table for each entity, with attributes as columns and a primary key for unique identification.                                                           |
| **1-to-1 Partial-Partial**      | 1. Use the primary key of one **table** **as a foreign key in the other**.<br> 2. Create a **new table** with the primary keys of both tables as foreign keys.    |
| **1-to-1 Total-Partial**        | Use the primary key of the partial side as a foreign key in the total side.                                                                                       |
| **1-to-1 Total-Total**          | Merge both tables into a single table, as both sides are mandatory.                                                                                               |
| **1-to-Many**                   | 1. Add the primary key of the "1" side as a foreign key in the "many" side.<br> 2. Create a new table with the primary keys of both tables as foreign keys.       |
| **Many-to-Many**                | Create a new table (join table) with the primary keys of both tables as foreign keys, establishing a many-to-many relationship.                                   |
| **Weak Entities**               | Create a table for the weak entity, including a foreign key from the supporting entity and a composite primary key (using the foreign key and unique attributes). |
| **Multivalued Attributes**      | Use a separate table for each multivalued attribute, with a foreign key linking it back to the main entity’s table. Each value is stored as a new row.            |
| **Derived Attributes**          | Exclude from the database schema; calculate dynamically as needed through queries or views.                                                                       |

### 1. Mapping of regular(Strong) Entity Types
![[Pasted image 20241108070613.png]]
### 2. Mapping of Multivalued Attributes
الـ Complex Attribute زيها برضو بالظبط
![[Pasted image 20241108070927.png]]
![[4.jpeg]]
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
### 4. Mapping of Weak Entity Type
![[Pasted image 20241108075450.png]]
![[Pasted image 20241108075459.png]]