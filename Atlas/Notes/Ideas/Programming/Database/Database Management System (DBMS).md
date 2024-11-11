---
up:
  - "[[Database MOC]]"
related:
  - "[[Database]]"
created: 2024-05-20
---
# Database Management System (DBMS)
- A __database Management System (DBMS)__ is a software that enables users to _create, maintain, and access_ databases.
- Its features allow us to manage the data in an efficient and easy manner.
- An __application program__ access the database by sending queries or requests to the DBMS.
## Why use DBMS?
### Files as storage
![[Database#File as storage (File Base System)]]

### DBMS  Functionalities
![[Pasted image 20241111052946.png]]
### Advantages of DBMS
![[Pasted image 20240520160437.png]]
![[Pasted image 20240520160445.png]]
### We also talked about [[Database#Database is __acid__|acid]]
![[Database#Database is __acid__|acid]]
## DBMS Terminologies

### Data Model
مجموعة من المفاهيم المستخدمة لوصف البيانات في قاعدة البيانات. 
النماذج الأكثر استخدامًا:
1. الـ[[Conceptual Data Model]]: يعرض البيانات بشكل قريب من تصورات المستخدمين، مثل **Entity-Relationship Model** و**Object-Based Model**.
2. الـ**Physical Data Model**: يعرض تفاصيل تخزين البيانات مثل **record formats** و**access paths**.
3. الـ**Implementation (Representational) Data Model**: يدمج بين النماذج السابقة، ويُستخدم في نظم إدارة قواعد البيانات التجارية، مثل **relational data model**.

![[Pasted image 20241025102627.png]]
### Schema
وصف لهيكل البيانات باستخدام **Data Model**، ويشمل وصف **الحقول** و**القيود** على البيانات.

- الـ**Conceptual Schema**: يصف البيانات المخزنة في قاعدة البيانات.
- الـ**Physical Schema**: يحدد تفاصيل تخزين البيانات على الهارد.
- الـ**External Schema**: يسمح بإنشاء عدة نماذج خارجية توفر وصول مخصص لمجموعات مختلفة من المستخدمين.

![[Pasted image 20241025102707.png]]
![[Pasted image 20241025102741.png]]
### Levels of Abstraction in a DBMS
يتم وصف البيانات في ثلاثة مستويات:
- __Conceptual Schema__: describes the stored data in terms of the data model of the DBMS.
- __Physical Schema__: specifies data storage details (تخزينها فعليًا على الهارد)
- __External Schema__: We can define different external schemas to give customized access to different users and groups.


![[Pasted image 20240520161241.png]]
![[Pasted image 20241025102830.png]]
## Popular DBMS

![[Pasted image 20240520161632.png]]