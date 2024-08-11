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
### File as storage
- Try to store the data in a text file .. simple and easy!
##### File Based System
- زمان مكنوش بيخزنوا ال Data في DB كانو بيخزنوها في Files
- انك مثلا تحط الباسووردات بتاعك في txt أو انك تخزن أسماء المغنيين في فايل وفايل تاني أحط فيه أسماء الألبومات اللي عملها كل مغني
- بس عشان تقرأ الفايلات دي كان عندي نوعين من ال Files :
1. Delimited File:
    Delimiter ودا المقصود بيها ان انت بتفصل بين كل حاجة وحاجة تانية بكوما مثلا او نقطة

2. Fixed Width File
    انك تحدد عدد بايتس لكل حاجة بتدخلها

![[Pasted image 20240520170051.png]]
###### مميزاتها
- رخيص جدا
###### عيوبها
- الوصول للداتا صعب جدا (Read- Write - Update ..) ودا معناه ان ال Website هيبقا بطيء
- عندي نسخ مختلفة من الداتا دي لو كذا حد شغال عليها
    - فكل واحد هيعدل مش هيشوف التعديل بتاع التاني وهيبقا عندي كدا نسخ مختلفة
- معنديش علاقة بين الفايلات وبعض يعني لو دخلت معلومات غلط هيقبلها عادي حتى لو المعلومة دي ملهاش علاقة بالفايل التاني
- مفيش DB Integrity
    - ان الداتا تسمع على بعض
##### Data Redundancy
- مشكلة تكرار الداتا
  يعني لو غيرت الداتا في فايل ما وانت عندك كذا نسخة من الفايل فلازم تروح تغيره في كل الفايلات

![[Pasted image 20240520154419.png]]

- انما لو عندي DB المفروض التغيير اللي بيحصل بيسمع في النسخة الأصلية فالبتالي مش هحتاج أغير في كله
##### Data Administration
- ان مش أي حد يقدر يعدل أي داتا لأن دا مينفعش 
  مينفعش المدرس يعدل رواتب الموظفين

![[Pasted image 20240520155157.png]]
##### Efficient Data Access
- في الفايل مش بقدر أوصل للداتا بسهولة وبيبقا صعب جدا أوصل لأي حاجة محتاجها

![[Pasted image 20240520155339.png]]
##### Concurrent Access
- انك تقدر تدخل على الداتا في نفس الوقت وتقدر تعمل تغييرين في نفس الوقت

![[Pasted image 20240520155656.png]]
##### Crash Recovery
- لو حصل كراش لأي سبب المفروض ايه اللي يحصل
- أكيد في الفايل الداتا كلها هتطير

![[Pasted image 20240520155754.png]]
##### Data Integrity
- تكامل البيانات: ان مينفعش تحط رقم مثلًا في الدرجات

![[Pasted image 20240520160046.png]]
##### Data Security
- لو حد هكر الداتا وعمل remove هيمسح كل الداتا بتاعتي

![[Pasted image 20240520160145.png]]
##### Reduced Application Development time
- معدتش بتفكر فازاي تجيب الداتا 
- انك ترتب داتا اللي في الفايل
- ازاي تتعامل لما يحصل كراش

![[Pasted image 20240520160301.png]]

### Advantages of DBMS
![[Pasted image 20240520160437.png]]
![[Pasted image 20240520160445.png]]
### We also talked about [[Database#Database is __acid__|acid]]
## DBMS Terminologies
- شوية مصطلحات مهمة في ال DBMS
### Data Model
- It's a collection of concepts used for describing data
- It hides many low-level storage details
- Most DBMSs today are based on the __relational data model__
### Schema
- It's a description of data in terms of a data model.
## Levels of abstraction in a DBMS
- Data in a DBMS is described at three levels of abstraction: _Conceptional, physical, and external_

![[Pasted image 20240520161241.png]]
- __Conceptual Schema__: describes the stored data in terms of the data model of the DBMS.
- __Physical Schema__: specifies data storage details.
- __External Schema__: We can define different external schemas to give customized access to different users and groups.


## Popular DBMS
![[Pasted image 20240520161632.png]]