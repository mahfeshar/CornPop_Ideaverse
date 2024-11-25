---
up:
  - "[[Database MOC]]"
related: 
created: 2024-11-04
---

![[Pasted image 20241029203429.png]]
اتكلمنا عنها قبل كدا في الـ [[DB Life Cycle]]

أول حاجة هناخد المعلومات من الخطوة اللي قبلها على هيئة ملف فيه كل المعلومات عن الأبلكيشن **SRS**
![[Pasted image 20241029203532.png]]
## Conceptual Design (ERD)
### Entity
- عبارة عن **Object** أو شيء في الـ Real World
- ممكن يبقا له وجود فعلي **Physical** زي Car أو ممكن يبقا Concept أو **Conceptual** زي Course
- كل Entity بيبقا فيه مجموعة من الـ **Attributes** وهي شوية Properties بتوصفه
- ممكن يبقا عندي مجموعة من الـ Entities زي Cars وبنقل عليه **Entity Set** وبنسمي كل واحدة في الـ Set اسمها **Instance**

![[Pasted image 20241029204413.png]]
#### Weak Entity
لو أنا عندي في الـ System اتنين Entity الـ Employee والـ Childs بتوعه
فلو مثلًا الموظف اتمسح المفروض نمسح ولاده ولا لا؟ فدا على حسب **حاجة العميل** 
فيه ناس زي مؤسسة عسكرية محتاجين يحتفظوا بيها (**Strong**)
لو هيتمسح معاه يبقا دا الـ (**Weak**) لأنه معتمد على Entity تانية
![[Pasted image 20241029211658.png]]
فيه حاجة كمان بتترسم هنا وهي الـ Partial Key اللي هي تحتها خط منقط دا
### Attributes
- هي **الصفات** اللي بتوصف الـ Entity 
- ليها أنواع كتير:

![[Pasted image 20241029204751.png]]
- ممكن يبقا عندي Attribute يبقا له أكثر من نوع بيبقا اسمه (**Complex**)
	- زي الرقم ممكن يتقسم لـ Code و Number فكدا بقا Composite وكمان ممكن يبقا Multivalued فدا بنسميه **Complex**
#### ليه لو اليوزر عايز يدخل 3 أرقام تليفون معملش Composite مش Multivalued؟

### Relationships
- العلاقات بين الـ Entities وبعض
- ممكن الـ Relation تبقا عندها Attributes
	- بنعملها لو الـ Attribute له علاقة بالـ Verb (On Relation Attribute) 
	  بمعنى كل أما الـRelation تحصل، فيه معلومات بتظهر

![[Pasted image 20241029205324.png]]
فيه عندنا 3 تعريفات للـ Relationship:
1. Degree (Unary - Binary - Ternary)
2. Cardinality Ratio (1:1 - 1:M - M:N)
3. Participation (Total "Must" - Partial "May")
#### Degree
الـ(عدد المشاركين في العلاقة) **Degree** ممكن تبقا:
- Unary
- Binary
- Ternary

#### Participation Constraints
هل الـ Entity هتشارك في العلاقة ولا لا؟
![[Pasted image 20241029212512.png]]
#### Cardinality Ratio
![[Pasted image 20241029211240.png]]
![[Pasted image 20241029211259.png]]
![[Pasted image 20241029211309.png]]
![[Pasted image 20241029211321.png]]
### Symbols
![[Pasted image 20241029214357.png]]
- جنب الـ ERD بنسلم فايل بيبقا فيه Equations زي مثلًا حساب الـ Derived Attributes أو طريقة كتابة الـ Composite 
	- لو هحسب العمر من تاريخ الميلاد فدا هيبقا Derived عشان كدا لازم أديله معادلة الحساب وهكذا لو الإسم بيتكون من Fname , Lname لازم أقوله هتتكتب ازاي

### Examples
#### University Database
![[Pasted image 20241030071120.png]]
![[Pasted image 20241030071131.png]]
![[Pasted image 20241030073203.png]]

#### Company Database
![[Pasted image 20241030072840.png]]
![[Pasted image 20241030102458.png]]
#### Premier League Database
![[Pasted image 20241030072905.png]]
![[Pasted image 20241030102513.png]]
#### Library Database (Task)
![[Pasted image 20241030072929.png]]