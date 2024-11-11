---
up:
  - "[[Database MOC]]"
related:
  - "[[Database Management System (DBMS)]]"
created: 2024-05-21
---
## What are databases for?
البرنامج بتاعنا بياخد Input وبيعمل Process ليها وبيطلع Output بس كل دا بيحصل في الميموري وبمجرد ما البرنامج يقفل الداتا دي بتطير
فيه برامج مش بيفرق معانا اننا نخزن الداتا دي عادي (الآلة حاسبة) 
وفيه برامج لا محتاج أخزن الداتا دي (تسجيل كورسات)

![[Pasted image 20241105120657.png]]
- Storing data in your application (in memory) has the obvious shortcoming that, whatever the technology you’re using, **your data dies when your server stops**. 
- Some programming languages and/or frameworks take it even further by being **stateless**, which, in the case of an HTTP server, means your data dies at the end of an HTTP request. 
- Whether the technology you’re using is stateless or stateful, you will need to persist your data somewhere. That’s what databases are for.

## Data vs Information
Data: شوية البيانات اللي انا **بجمعها**
Information: لما بعمل على الداتا بروسيسينج بتتحول لمعلومة

مثال: تاريخ الميلاد يعتبر **Data** هعمل عليه Process فهيتحول لعمر فدي **Information**
## File as storage (File Base System)
- Try to store the data in a text file .. simple and easy!
- زمان مكنوش بيخزنوا ال Data في DB كانو بيخزنوها في Files
- انك مثلا تحط الباسووردات بتاعك في txt أو انك تخزن أسماء المغنيين في فايل وفايل تاني أحط فيه أسماء الألبومات اللي عملها كل مغني
### 2 Ways to save data in files
بس عشان تقرأ الفايلات دي كان عندي نوعين من ال Files :
1. Delimited File:
    Delimiter ودا المقصود بيها ان انت بتفصل بين كل حاجة وحاجة تانية بكوما مثلا او نقطة

2. Fixed Width File
    انك تحدد عدد بايتس لكل حاجة بتدخلها

![[Pasted image 20240520170051.png]]
### مميزاتها
- رخيص جدا
### عيوبها
![[Pasted image 20241111034824.png]]
- الوصول للداتا صعب جدا (Read- Write - Update ..) ودا معناه ان ال Website هيبقا بطيء
- البحث عن الداتا بيباخد وقت طويل لأنه بياخد الفايل من أوله لآخره وهكذا
- عندي نسخ مختلفة من الداتا دي لو كذا حد شغال عليها
    - فكل واحد هيعدل مش هيشوف التعديل بتاع التاني وهيبقا عندي كدا نسخ مختلفة
- معنديش علاقة بين الفايلات وبعض يعني لو دخلت معلومات غلط هيقبلها عادي حتى لو المعلومة دي ملهاش علاقة بالفايل التاني
- مفيش DB Integrity
    - ان الداتا تسمع على بعض
#### Data Redundancy (تكرار الداتا)
- مشكلة تكرار الداتا
  يعني لو غيرت الداتا في فايل ما وانت عندك كذا نسخة من الفايل فلازم تروح تغيره في كل الفايلات

![[Pasted image 20240520154419.png]]

- انما لو عندي DB المفروض التغيير اللي بيحصل بيسمع في النسخة الأصلية فالبتالي مش هحتاج أغير في كله
#### Data Administration (أي حد يقدر يعدل ويوصل لأي حاجة)
- ان مش أي حد يقدر يعدل أي داتا لأن دا مينفعش 
  مينفعش المدرس يعدل رواتب الموظفين
- كل موظف المفروض يبقا له وصول لجزء معين من البيانات مش كلها عشان ميعدلش عليها

![[Pasted image 20240520155157.png]]
#### Efficient Data Access (الوصول الصعب للداتا)
- في الفايل مش بقدر أوصل للداتا بسهولة وبيبقا صعب جدا أوصل لأي حاجة محتاجها
- فلو احتاجت أدور على حاجة معينة لازم أمشي على كل اللي قبلها وادور واحدة واحدة

![[Pasted image 20240520155339.png]]
#### Concurrent Access (أكتر من حد يعدل في نفس الوقت)
- انك تقدر تدخل على الداتا في نفس الوقت وتقدر تعمل تغييرين في نفس الوقت

![[Pasted image 20240520155656.png]]
#### Crash Recovery (لو عطل في النص متقدرش ترجع)
- لو حصل كراش لأي سبب المفروض ايه اللي يحصل
- أكيد في الفايل الداتا كلها هتطير

![[Pasted image 20240520155754.png]]
#### Data Integrity (تقدر تحط أي داتا في أي حتة حتى لو غلط)
- تكامل البيانات: ان مينفعش تحط رقم مثلًا في الدرجات

![[Pasted image 20240520160046.png]]
#### Data Security (لو حد مسح الفايل كل الداتا راحت)
- لو حد هكر الداتا وعمل remove هيمسح كل الداتا بتاعتي

![[Pasted image 20240520160145.png]]
#### Reduced Application Development time
- معدتش بتفكر فازاي تجيب الداتا 
- انك ترتب داتا اللي في الفايل
- ازاي تتعامل لما يحصل كراش

![[Pasted image 20240520160301.png]]


## Database
- It's for everyone (Backend Developer, Mobile Application Developer, Data Scientist).
- A __database__ is a *collection of data*, typically describing the activities of one or more related organizations.
- A __database__ _models_ some aspect of the real world (student, course)
- A database can be of __any size__ or __complexity__
- تقدر تقول انها شوية داتا (فايلات) مربوطة ببعض
- اللي بيربط الداتا دي (الفايلات) هو نظام إدارة قواعد البيانات [[Database Management System (DBMS)]] ودي بتبقا زي Layer بين الـ Database and Program
  نقدر نقول انه مجرد **منظم** للعملية دي
## Database is __acid__
- **A**tomicity: transactions are atomic, which means if a transaction fails, the result will be like it never happened.
- **C**onsistency: you can define rules for your data, and expect that the data abides by the rules, or else the transaction fails.
- **I**solation: run two operations at the same time, and you can expect that the result is as though they were ran one after the other. 
  That’s not the case with the JSON file storage you built: if 2 insert operations are done at the same time, the later one will fetch an outdated collection of users because the earlier one is not finished yet, and therefore overwrite the file without the change that the earlier operation made, totally ignoring that it ever happened.
- **D**urability: unplug your server at any time, boot it back up, and it didn’t lose any data.

## __ACID__ is a cool acronym! [[CRUD]] is another cool one
## [[Database Management System (DBMS)]]