---
up:
  - "[[Database MOC]]"
related:
  - "[[Database Management System (DBMS)]]"
created: 2024-05-21
---
## What are databases for?
![[Pasted image 20241105120657.png]]
البرنامج بياخد Input وبيعمل Processing ليها وبيطلع Output، لكن كل دا بيحصل في الذاكرة. بمجرد ما يقفل البرنامج، الداتا بتطير.

فيه برامج مش بيفرق معانا نخزن الداتا (زي الآلة الحاسبة) وفيه برامج محتاجين نخزن الداتا زي تسجيل الكورسات.

- تخزين الداتا داخل التطبيق (في الذاكرة) بيخلي الداتا تضيع لو السيرفر وقف.
- بعض اللغات أو الفريموركات بتكون **stateless**، وده يعني إن الداتا بتموت مع نهاية الـ HTTP request.
- بغض النظر عن Technology، لازم نحافظ على الداتا في مكان دائم. وهنا بيجي دور قواعد البيانات.
## Before Begin
### Data vs Information
- الـ**Data:** شوية البيانات اللي أنا **بجمعها**.
- الـ**Information:** لما بعمل على الداتا بروسيسينج، بتتحول لمعلومة.
مثال: تاريخ الميلاد يعتبر **Data**، ولو عملت بروسيسينج ليه هيطلع لي العمر ودي تعتبر **Information**.
### File as storage (File Base System)
- كان الناس بيحاولوا يخزنوا الداتا في ملفات نصية، وكان الموضوع بسيط وسهل!
- في البداية، كانوا بيخزنوا الداتا في ملفات بدل قواعد البيانات، زي تخزين الباسووردات في ملف txt أو تخزين أسماء المغنيين في ملف وأسماء الألبومات في ملف تاني.
### 2 Ways to save data in files
عشان تقرأ الفايلات دي كان عندي نوعين من الفايلات:

1. الـ**Delimited File:** بفصل بين كل حاجة بكوما أو نقطة.
2. الـ**Fixed Width File:** بحدد عدد البايتس لكل Input.

![[Pasted image 20240520170051.png]]
#### مميزات التخزين في ملفات
- رخيص جدا
#### عيوبها
- **صعوبة الوصول للداتا:** القراءة والكتابة والتحديث بيخلي الموقع بطيء.
- **البحث بيطول:** لأن الفايل بيتقرأ من أوله لآخره.
- **تكرار الداتا (Data Redundancy):** لو فيه كذا حد بيشتغل على نسخة، مش هيقدر يشوف التعديلات الجديدة.
![[Pasted image 20240520154419.png]]
- **عدم وجود علاقة بين الملفات:** لو دخلت بيانات غلط، هيقبلها عادي حتى لو مالهاش علاقة.
- **عدم وجود تكامل في الداتا (Data Integrity):** يعني الداتا مش بتسمع على بعض.
![[Pasted image 20240520160046.png]]
- **التحكم في الوصول (Data Administration):** مش أي حد يعدل أو يوصل لأي داتا.
![[Pasted image 20240520155157.png]]
- **الوصول الصعب للداتا (Efficient Data Access):** الوصول لأي حاجة بيبقى صعب جدا.
![[Pasted image 20240520155339.png]]
- **التعامل المتزامن (Concurrent Access):** مشكلة إن أكتر من شخص يعدل في نفس الوقت.
![[Pasted image 20240520155656.png]]
- **التعافي بعد العطل (Crash Recovery):** لو حصل كراش، الداتا هتطير.
![[Pasted image 20240520155754.png]]
- **أمان الداتا (Data Security):** لو حد مسح الفايل كله، الداتا راحت.
![[Pasted image 20240520160145.png]]
- **تقليل وقت تطوير التطبيق (Reduced Application Development time):** مش بتفكر في ازاي تجيب الداتا أو تتعامل مع الكراش.
![[Pasted image 20240520160301.png]]
### Database vs Spreadsheet
قواعد البيانات وجداول البيانات (زي Excel) بيخزنوا المعلومات لكن بشكل مختلف. الفروقات الأساسية بينهم هي:

- طريقة تخزين الداتا ومعالجتها.
- مين يقدر يوصل للداتا.
- حجم الداتا الممكن تخزينه.

الجداول الإلكترونية بتتصمم لمستخدم واحد، وبتكون سهلة وصغيرة في الداتا. 
قواعد البيانات بتدعم تخزين **كميات كبيرة** وبتسمح بوصول متعدد ومضمون للأمان.
## Database
- It's for everyone (Backend Developer, Mobile Application Developer, Data Scientist).
- A __database__ is a *collection of data*, typically describing the activities of one or more related organizations.
  تقدر تقول انها شوية داتا (فايلات) مربوطة ببعض
- A __database__ _models_ some aspect of the real world (student, course)
- A database can be of __any size__ or __complexity__
- اللي بيربط الداتا دي (الفايلات) هو نظام إدارة قواعد البيانات [[Database Management System (DBMS)]] ودي بتبقا زي Layer بين الـ Database و Program
  نقدر نقول انه مجرد **منظم** للعملية دي
## Types of databases
كل مؤسسة بتحتاج قاعدة بيانات معينة حسب استخدام الداتا.
#### Relational databases
مرتبة كجداول من أعمدة وصفوف، وتعتبر الأكثر كفاءة.
#### Object-oriented databases
المعلومات بتمثل على هيئة كائنات (Objects).
#### Distributed databases
موزعة على مواقع مختلفة. 
زي [[Intro to Distributed systems|Distributed systems]].

#### Data warehouses
مخزن مركزي للداتا، ومصمم للبحث والتحليل السريع.
#### NoSQL databases
بيسمح بتخزين الداتا غير المنظمة، وبيشتهر مع التطبيقات الويب المعقدة.
#### Key-Value Database
![[Pasted image 20241112184841.png]]
مثال: Redis, Memcached
#### Graph databases
بتخزن الداتا ككيانات وعلاقات بينهم.

![[Pasted image 20241112185109.png]]
#### OLTP databases
صممت لمعالجة المعاملات السريعة والتحليل الكبير.
#### Open source databases
النظام مفتوح المصدر، وممكن يكون SQL أو NoSQL.
#### Cloud databases
قاعدة بيانات موجودة على السحاب، وبتكون إما تقليدية أو Database as a Service (DBaaS).
#### Multimodel database
بتجمع بين نماذج مختلفة من قواعد البيانات.
#### Document/JSON database
بتدير الداتا بشكل JSON بدلاً من الصفوف والأعمدة.

![[Pasted image 20241112185022.png]]
#### Self-driving databases
قواعد بيانات تعتمد على الذكاء الاصطناعي لتفعيل الصيانة والتحديثات والأمان تلقائيًا.
## Database is __acid__
- **Atomicity:** المعاملات بتكون ذرية، لو المعاملة فشلت كأنها لم تحدث.
- **Consistency:** الداتا لازم تتبع القواعد المحددة، وأنت اللي بتحدد القواعد دي.
- **Isolation:** تقدر تنفذ عمليتين في نفس الوقت وكأنهم واحد وراء التاني.
- **Durability:** الداتا مش بتضيع حتى لو السيرفر فصل.
- **C**onsistency: you can define rules for your data, and expect that the data abides by the rules, or else the transaction fails.
- **I**solation: run two operations at the same time, and you can expect that the result is as though they were ran one after the other. 
  That’s not the case with the JSON file storage you built: if 2 insert operations are done at the same time, the later one will fetch an outdated collection of users because the earlier one is not finished yet, and therefore overwrite the file without the change that the earlier operation made, totally ignoring that it ever happened.
- **D**urability: unplug your server at any time, boot it back up, and it didn’t lose any data.

## __ACID__ is a cool acronym! [[CRUD]] is another cool one
## [[Database Management System (DBMS)]]