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
## Before Begin
### Data vs Information
Data: شوية البيانات اللي انا **بجمعها**
Information: لما بعمل على الداتا بروسيسينج بتتحول لمعلومة

مثال: تاريخ الميلاد يعتبر **Data** هعمل عليه Process فهيتحول لعمر فدي **Information**
### File as storage (File Base System)
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
#### مميزاتها
- رخيص جدا
#### عيوبها
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



### Database vs Spreadsheet
Databases and spreadsheets (such as Microsoft Excel) are both convenient ways to store information. The primary differences between the two are:

- How the data is stored and manipulated
- Who can access the data
- How much data can be stored

Spreadsheets were originally designed for one user, and their characteristics reflect that. They’re great for a single user or small number of users who don’t need to do a lot of incredibly complicated data manipulation. 
Databases, on the other hand, are designed to hold **much larger collections** of organized information, massive amounts, sometimes. 
Databases allow multiple users at the same time to quickly and securely access and query the data using highly complex logic and language.
## Database
- It's for everyone (Backend Developer, Mobile Application Developer, Data Scientist).
- A __database__ is a *collection of data*, typically describing the activities of one or more related organizations.
- A __database__ _models_ some aspect of the real world (student, course)
- A database can be of __any size__ or __complexity__
- تقدر تقول انها شوية داتا (فايلات) مربوطة ببعض
- اللي بيربط الداتا دي (الفايلات) هو نظام إدارة قواعد البيانات [[Database Management System (DBMS)]] ودي بتبقا زي Layer بين الـ Database and Program
  نقدر نقول انه مجرد **منظم** للعملية دي
- A database is usually controlled by a [[Database Management System (DBMS)]]. 
- Together, the data and the DBMS, along with the applications that are associated with them, are referred to as a database system, often shortened to just database.
- Data within the most common types of databases in operation today is typically modeled in rows and columns in a series of tables to make processing and data querying efficient. 
- The data can then be easily accessed, managed, modified, updated, controlled, and organized. Most databases use structured query language (SQL) for writing and querying data
## Types of databases
There are many different types of databases. The best database for a specific organization depends on how the organization intends to use the data.

#### Relational databases

- [Relational databases](https://www.oracle.com/ca-en/database/what-is-a-relational-database/) became dominant in the 1980s. Items in a relational database are organized as a set of tables with columns and rows. Relational database technology provides the most efficient and flexible way to access structured information.

#### Object-oriented databases

- Information in an object-oriented database is represented in the form of objects, as in object-oriented programming.

#### Distributed databases

- A distributed database consists of two or more files located in different sites. The database may be stored on multiple computers, located in the same physical location, or scattered over different networks.
- Like in [[Intro to Distributed systems|Distributed systems]]
- 

#### Data warehouses

- A central repository for data, a data warehouse is a type of database specifically designed for fast query and analysis.

#### NoSQL databases

- A [NoSQL](https://www.oracle.com/ca-en/database/nosql/), or nonrelational database, allows unstructured and semistructured data to be stored and manipulated (in contrast to a relational database, which defines how all data inserted into the database must be composed). NoSQL databases grew popular as web applications became more common and more complex.

#### Key Value Database
![[Pasted image 20241112184841.png]]
**Examples:** Redis, Memcached etc.
#### Graph databases

- A graph database stores data in terms of entities and the relationships between entities.
- **OLTP databases.** An OLTP database is a speedy, analytic database designed for large numbers of transactions performed by multiple users.

These are only a few of the several dozen types of databases in use today. Other, less common databases are tailored to very specific scientific, financial, or other functions. In addition to the different database types, changes in technology development approaches and dramatic advances such as the cloud and automation are propelling databases in entirely new directions. Some of the latest databases include

![[Pasted image 20241112185109.png]]
#### Open source databases

- An open source database system is one whose source code is open source; such databases could be SQL or NoSQL databases.

#### Cloud databases

- A [cloud database](https://www.oracle.com/ca-en/database/what-is-a-cloud-database/) is a collection of data, either structured or unstructured, that resides on a private, public, or hybrid cloud computing platform. There are two types of cloud database models: traditional and database as a service (DBaaS). With DBaaS, administrative tasks and maintenance are performed by a service provider.

#### Multimodel database

- Multimodel databases combine different types of database models into a single, integrated back end. This means they can accommodate various data types.

#### Document/JSON database

- Designed for storing, retrieving, and managing document-oriented information, [document databases](https://www.oracle.com/ca-en/autonomous-database/autonomous-json-database/) are a modern way to store data in JSON format rather than rows and columns.

![[Pasted image 20241112185022.png]]
#### Self-driving databases

- The newest and most groundbreaking type of database, self-driving databases (also known as autonomous databases) are cloud-based and use machine learning to automate database tuning, security, backups, updates, and other routine management tasks traditionally performed by database administrators.

[Learn more about self-driving databases](https://www.oracle.com/ca-en/autonomous-database/what-is-autonomous-database/)
## Database is __acid__
- **A**tomicity: transactions are atomic, which means if a transaction fails, the result will be like it never happened.
- **C**onsistency: you can define rules for your data, and expect that the data abides by the rules, or else the transaction fails.
- **I**solation: run two operations at the same time, and you can expect that the result is as though they were ran one after the other. 
  That’s not the case with the JSON file storage you built: if 2 insert operations are done at the same time, the later one will fetch an outdated collection of users because the earlier one is not finished yet, and therefore overwrite the file without the change that the earlier operation made, totally ignoring that it ever happened.
- **D**urability: unplug your server at any time, boot it back up, and it didn’t lose any data.

## __ACID__ is a cool acronym! [[CRUD]] is another cool one
## [[Database Management System (DBMS)]]