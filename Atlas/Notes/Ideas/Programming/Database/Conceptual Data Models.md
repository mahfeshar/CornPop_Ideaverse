---
up:
  - "[[Database MOC]]"
related: 
created: 2024-11-11
---
اتكلمنا عنها في الـ [[Database Management System (DBMS)#Data Model|Data Models]]

مبيهمنيش بتتخزن ازاي على الهارد إنما بيهمني هي تبظهر ازاي وبتشتغل إزاي
يعني بيهمني همثل الداتا بيز ازاي، أو اللوجيك اللي في دماغي: هي هتتمثل إزاي؟
من حيث الـ Concept أو Logic
### 1. Hierarchical Model
- This is one of the oldest models in a data model which was developed by IBM, in the 1950s.
- بنبصلها بحاجة شبيهه بالـ Tree، فبيبقا ليه root وبيحصلها تفرعات
- Navigational databases such as the hierarchical database (which relied on a tree-like model and allowed only a one-to-many relationship)
**Example 1:** Consider the below Student database system hierarchical model.
![[Pasted image 20241111083543.png]]
#### عيوبه:

1. **معقد في التطبيق**: رغم سهولته كفكرة، لكنه صعب التنفيذ.
2. **مش مرن**: أي تعديل ممكن يكون معقد ويؤدي لمسائل في إدارة النظام.
3. **مفيش معايير ثابتة** للتطبيق؛ لأنه ملوش standards موحدة.
4. **محدود**: مش بيدعم كل العلاقات، لأنه بيطلب علاقات من نوع 1 فقط.

### 2. Network Model
نموذج في قواعد البيانات بيسمح بتمثيل علاقات **many-to-many** بشكل مرن ومعقد أكتر من النموذج الهرمي. 
بيعتمد على بنية تشبه **الجراف** (graph structure) اللي بيكون فيه عقد (nodes) بتمثل الكيانات، وحواف (edges) بتمثل العلاقات بين الكيانات.

![[Pasted image 20241111085700.png]]
**Example :** Network model for a Finance Department.

Below we have designed the network model for a Finance Department:
![[Pasted image 20241111085743.png]]
#### مميزات النموذج الشبكي

1. بيسمح بتمثيل علاقات معقدة زي **1:1**، **1: M**
2. سهل الوصول للبيانات من خلال المالك أو العضو.
3. بيدعم تكامل البيانات بفضل علاقات المالك-العضو.

#### عيوب النموذج الشبكي
1. بنية قاعدة البيانات معقدة وصعبة في التصميم بسبب استخدام المؤشرات.
2. تنفيذ معقد بسبب وجود مؤشرات للملاحة.
3. مفيش معايير ثابتة للنموذج.
4. ما بيدعمش تحسين الاستعلامات بشكل تلقائي.

#### الفرق بين النموذج الهرمي والنموذج الشبكي

|الخاصية|النموذج الهرمي|النموذج الشبكي|
|---|---|---|
|الهيكل|هيكل شجري|هيكل جراف|
|العلاقات|واحد إلى متعدد|متعدد إلى متعدد|
|المرونة|أقل مرونة|أكثر مرونة|
|الوصول للبيانات|مسار وصول واحد|مسارات وصول متعددة|
|التكرار|تكرار أعلى|تكرار أقل بفضل العلاقات المشتركة|
|التعقيد|بسيط|أكثر تعقيد|
|سيناريو الاستخدام|مناسب للبيانات البسيطة|مناسب للبيانات المعقدة|
|الكفاءة|فعال في التصفح الهرمي|فعال في الاستعلامات المعقدة|
### 3. Relational Model (**الأشهر**)
نموذج يوضح كيفية تخزين البيانات في (RDBMS)، حيث يتم تخزين البيانات في شكل جداول (**Relations**) تمثل كل منها كيانًا معينًا بخصائص مختلفة. 
كل جدول يتكون من صفوف وأعمدة، وكل عمود يحمل اسم فريد يمثل خاصية (Attribute).

|ROLL_NO|NAME|ADDRESS|PHONE|AGE|
|---|---|---|---|---|
|1|RAM|DELHI|9455123451|18|
|2|RAMESH|GURGAON|9652431543|18|
|3|SUJIT|ROHTAK|9156253131|20|
|4|SURESH|DELHI||18|
#### مصطلحات هامة
![[Pasted image 20241111091840.png]]
- الـ **Table** (entity): مجموعة من الـ Records
- الـ**Attribute** (Columns - Field): الخاصيات التي تحدد الكيان، مثل ROLL_NO وNAME.
- الـ**Tuple** (Record - Row): كل صف في الجدول يمثل Record.
- الـ **Cell**: تقاطع الـRow مع الـColumns
- الـ **Database**: مجموعة من الـ Tables
---
- الـ**Relation Schema**: المخطط الذي يوضح هيكل الجدول وخصائصه، مثل: 
  STUDENT (ROLL_NO, NAME, ADDRESS, PHONE, AGE)
- الـ**Relation Instance**: مجموعة من السجلات في جدول معين في وقت معين.
- الـ**Degree**: عدد Attributes في الجدول.
- الـ**Cardinality**: عدد Records في الجدول.
- الـ **Primary Key**: كل Record لازم يبقا عنده معلومة مميزة عن باقي الـ Records 
  (مينفعش يتكرر، شرط في الـ Relational DB)
### Evolution of the database
Databases have evolved dramatically since their inception in the early 1960s. Navigational databases such as the **hierarchical database** (which relied on a tree-like model and allowed only a one-to-many relationship), and the **network database** (a more flexible model that allowed multiple relationships), were the original systems used to store and manipulate data. 
Although simple, these early systems were inflexible. In the 1980s, **relational databases** became popular, followed by **object-oriented databases** in the 1990s. 
More recently, [[2+ Kinds of databases|NoSQL]]databases came about as a response to the growth of the internet and the need for faster speed and processing of unstructured data. Today, [cloud databases](https://www.oracle.com/ca-en/database/what-is-a-cloud-database/) and [self-driving databases](https://www.oracle.com/ca-en/database/what-is-database/#autonomous) are breaking new ground when it comes to how data is collected, stored, managed, and utilized.