---
up:
  - "[[Database MOC]]"
related: 
created: 2024-05-20
---
> هل لازم كل البرامج اللي في الدنيا يبقا ليها DB؟ لا مش لازم وفيه برامج ملهاش DB وممكن تبدلها بفايلات
بس معظم البرامج الكبيرة بتستخدم فيها ال DB
# Database Design Process

![[Pasted image 20240520164215.png]]
![[Pasted image 20240520164227.png]]
![[Pasted image 20240520164300.png]]
![[Pasted image 20240520164314.png]]

![[Pasted image 20241025102916.png]]
# DB Life Cycle
## 1. Analysis
- أول مشكلة هي انك تفهم أصلا ال client عايز يعمل ايه بالظبط
- دي أول حاجة اني بعمل Analysis وبشوف المطلوب ايه بالظبط؟
- بيبقا فيه شخص دي وظيفته انه بيشوف ال Scope بتاع ال DB وبيسلمني فايل Requirements Doc فيه كل المعلومات اللي انا محتاجها واسم الشخص دا System Analyst
- بيحل مشكلة ال gap اللي بين ال programmer وال Client لان المبرمج بيتكلم كود والعميل بيتكلم بيزنس
## 2. DB Design (ERD)
> فيه مقولة بتقول انك تشوف صورة احسن من انك تقرأ كتاب عشان بيوصلك معلومات اكتر
- في المرحلة دي بحول الكلام لرسمة بنسميها Entity Relationship Diagram (ERD)
  ودي بتبقا وظيفة ال DB designer
- بس مش هو ال DB
## 3. DB Mapping
- بنمرر ال Diagram اللي عملناه في المرحلة اللي فاتت في المرحلة دي ونعمله كذا حاجة
- هو عبارة عن Set of rules بتطبق على ال ERD فبطلع منه ال Actual Schema and Tables
  والمسؤول عنها هو برضو ال DB designer
- بعد ما بخلص المرحلة دي لازم أرجع لل System Analyst عشان أتأكد ان كل حاجة تمام وان الرسم بيحاكي الكلام اللي موجود في ال Requirements Doc
> ممكن نفس ال Requirements Doc يطلع منه أكتر من ERD
انما لو جيت تعمل Mapping لنفس ال ERD الناتج هيطلع نفسه دايمًا لأنها قواعد محفوظة
  

 > [!Note]
 > كل المراحل دي ممكن تتعمل على ورق بس (مجرد تفكير)
 > ودي مرحلة مهمة أوي انك تعمل Design عشان تبقا فاهم انت بتعمل ايه بالظبط انما مينفعش تبدأ تشتغل على طول
## 4. DB Implementation (Shared DB)
- دي اللي بحول فيها الكلام النظري Logical لحاجة فعليه أقدر أشتغل عليها Physical
- فهتحتاج Tool عشان تعمل المرحلة دي وهي [[Database Management System (DBMS)]]
  وأمثلة ليها: (SQL Server - Oracle - MySQL- Access …)
- وعشان تشتغل على أي tool من دي لازم تتعلم اللغة اللي اسمها [[Structured Query Language (SQL)]]
- والمسؤول عن المرحلة دي شخص اسمه DB Developer
---
- لما بتنزل SQL Server على جهازك، جهازك بيتحول ويبقا اسمه DB Server
- أي DB في الدنيا لازم تكون Shared ولو عندك نسختين مختلفين من نفس DB على جهازين مختلفين يبقا كدا اسمها Inconsistent DB
- انت في الحياة العملية بيبقا فيه Server واحد وكل اللي هيشتغلوا عليه بيعملوا Connect ويعدلو عليه
## 5. Application
- اني أستخدم ال DB بتاعي وأبدأ اوظفها في منتج فعلي ينفع ال Client يتعامل معاها
- اني أعمل GUI (Interface) زي مثلا Web Site - Mobile App - Desktop App
- وممكن تستخدم نفس ال DB في أكتر من حاجة
- وممكن أستخدمها بأي لغة وبأي شكل MVC - C# - Java - React
- واللي بيعمل المرحلة دي هو ال Application Programmer ودا نقدر نقول عليه انه DB User
## 6. Client → End User
- دا مش بيشوف ولا بيتعامل مع ال DB أصلا هو بيشوف البرنامج أو الموقع
- Browser → URL
- هو عبارة عن ال Application User

> End User click at URL → Application Server → app need Data → DB Server - taking data and going back
### مثال
عايز أعمل Website بينظم الحضور والإنصراف للموظفين
1. لازم ال System Analyst يقعد مع العميل ويشوفه هو عايز يعمل ايه بالظبط ويطلع Requirements Doc
2. ال DB Designer ياخد الفايل دا ويحوله لرسمة اسمها ERD
3. وبعدها نفس ال DB Designer يحول ال ERD ويعمله Mapping باني أطبق عليه مجموعة من ال rules عشان أطلع منه بال Actual Tables اللي المفروض تبقا موجودة جوا ال DB
4. هاخد كل اللي فات دا واديه ل DB Developer يحولي من حاجة نظرية لحاجة فعلية أقدر اوصلها واستخدمها
   وبستخدم في المرحلة دي Tool بيطلق عليها RDBMS زي ال SQL Server وبعمل ال Server دا على جهاز ويبقا دا ال DB Server بتاعي أقدر أستخدمه بعد كدا في ال DB دي واقدر اعمل Connect من كذا جهاز تاني
5. ال Client مبيتعاملش Direct مع ال DB دي فلازم يبقا فيه Interface العميل يقدر يتعامل معاها
   ودي مرحلة بناء ال Application وممكن يكون أي App واللي بيعمل المرحلة دي بقا ال Application Programmer وبيتخزن البرنامج دا في ال Application Server
وال programmer دا بنقول انه ال User بتاع ال DB فلو حب يستخدم ال DB دي بيستأذن ال Server اللي بيتحكم فيها ويقولها انا محتاج Data فبتديله الداتا اللي هو عايزها واللي بيعمل الدور دا هو ال DBMS

![[Pasted image 20240520163637.png]]