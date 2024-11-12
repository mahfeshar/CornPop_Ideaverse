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
![[Conceptual Data Models#3. Relational Model (**الأشهر**)]]
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

| Mapping Type                        | Solution                                    |
|-------------------------------------|---------------------------------------------|
| **1. Strong Entities**              | Create a new table for each strong entity   |
| **2. Weak Entities**                | Create a new table and add a foreign key for the strong entity |
| **3. Binary Relationships**         |                                             |
| - 1:1 Must-Must                     | Combine in one table (no new table needed)  |
| - 1:1 May-Must                      | Foreign key on the “Must” side (no new table needed) |
| - 1:1 May-May                       | Foreign key on either side (no new table needed) |
| - 1:M Must from "Many" side         | Foreign key on the "Many" side (no new table needed) |
| - 1:M May from "Many" side          | Foreign key on the "Many" side (no new table needed) |
| - M:N                               | Create a new linking table for the relationship |
| **4. Ternary Relationships**        | Create a new linking table with three foreign keys |
| **5. Unary Relationships**          | Use a self-referencing foreign key or create a new table depending on the relationship type |

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

### 3. Mapping Relationships
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

### 4. Mapping of N-ary Relationship
![[Pasted image 20241108092752.png]]
![[Pasted image 20241108092804.png]]
### 5. Mapping of Unary Relationship
بعملها في نفس الـ Table وأزود FK فيها بيشاور على  PK
دا في حالة الـ 1:M 

![[Pasted image 20241108102634.png]]
![[Pasted image 20241108102703.png]]

في حالة الـ M:N بنعمل Table جديدة بيبقا فيها اتنين FK بيشاوروا على نفس الـ PK
الحوار دا اسمه Junction Table
#### Junction Table
الـ **Junction Table** ببساطة هو جدول بنعمله في قواعد البيانات علشان نقدر نوصل بين جدولين عندهم علاقة **Many-to-Many**. 
طيب ليه بنحتاجه؟ لأن قاعدة البيانات ما تقدرش تعمل العلاقة دي مباشرة، فلازم نعمل جدول ثالث يوصل بينهم.

**طيب ناخد مثال بسيط؟**

خلينا نقول إن عندنا قاعدة بيانات للمدرسة، وعندنا جدولين رئيسيين:

1. جدول **Students** (الطلاب)، فيه بيانات عن كل طالب زي اسمه ورقم الطالب.
2. جدول **Courses** (المواد)، فيه بيانات عن كل مادة زي اسم المادة ورقم المادة.

طيب المشكلة هنا إن الطالب الواحد ممكن ياخد أكتر من مادة، والمادة الواحدة ممكن يكون فيها أكتر من طالب. يعني عندنا علاقة **Many-to-Many**.

**نحل المشكلة إزاي؟**

بنعمل جدول جديد نسميه **Students_Courses**، وده هو الـ Junction Table اللي هيوصل بين **Students** و**Courses**. 

في الجدول ده بنحط:

1. الـ`student_id`: ده زي المفتاح اللي بيربطنا بجدول **Students**.
2. الـ`course_id`: ده المفتاح اللي بيربطنا بجدول **Courses**.

شكل البيانات في الجدول

هتبقى بالشكل ده:

| student_id | course_id |
|------------|-----------|
| 1          | 101       |
| 1          | 102       |
| 2          | 101       |
| 3          | 103       |
