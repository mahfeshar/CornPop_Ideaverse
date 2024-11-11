---
up:
  - "[[Database MOC]]"
related: 
created: 2024-05-21
---
لما الناس بتتكلم عن **Databases**، غالبًا بيكون قصدهم **[[Conceptual Data Models#3. Relational Model (**الأشهر**)|Relationa]]** زي **PostgreSQL** و**MySQL** و**Oracle**. بس فيه أنواع تانية من **Databases** بتتسمى عمومًا **"NoSQL"**، ورغم إن الأنواع دي مختلفة عن بعضها، إلا إنها بتخدم أغراض كتير ومختلفة.

#### ليه اسمها "NoSQL"؟
الاسم **"NoSQL"** جاي من **SQL**، اللي هي اللغة اللي بنستخدمها عشان ندي أوامر (زي عمليات **CRUD** وإنشاء وحذف الجداول) في **Relational Databases**. الغريب بقا إن بعض قواعد **NoSQL** بتسمح باستخدام **SQL** برضه، وده بيخلي التسمية "NoSQL" شوية غريبة، بس لسه مشهورة وبنستخدمها عشان نفرّقها عن القواعد العلائقية.

#### شعبية قواعد **NoSQL**
في آخر كام سنة، قواعد **NoSQL** بقت مشهورة جدًا، لدرجة إن الناس كانت بتسأل هل هتستبدل **Relational Databases** بالكامل ولا لأ. لكن مع الوقت، السوق استقر وحصة **NoSQL** بقت ثابتة. النتيجة إن **NoSQL** بقت ناضجة ومستقرة، وبتستخدم في مشاريع كبيرة وصغيرة، بس **Relational Databases** لسه متربعة على العرش ومعظم المشاريع بتعتمد عليها.

#### ده معناه إيه لمهندسين البرمجيات؟
لو إنت مهندس برمجيات، لازم تكون فاهم **Relational Databases** كويس، لأنك غالبًا هتتعامل معاها في شغلك. وفي نفس الوقت، من المهم تكون عندك فكرة عن الأنواع المشهورة من **NoSQL Databases**، لأنك ممكن تحتاج تتعامل معاها برضه، حتى لو بشكل أقل.

- لما الناس بتتكلم عن ال DB بيبقا قصدهم على ال [[relational databases]] زي PostgreSQL, MySQL, Oracle
- بس فيه برضو أنواع تانية من ال DB المستخدمة في الصناعة واللي بيطلق عليها اسم [[NoSQL]] والاتنين دول ممكن يبقوا مختلفين عن بعض تمامًا والتانية بتخدم حاجات مختلفة
- الاسم NoSQL جاي من SQL وهي ال Syntax اللي بتخلينا نعمل [[CRUD]]
- بعض ال Non-relational databases اللي بنقول عليها NoSQL بتديلنا option اننا نستخدم [[Structured Query Language (SQL)|SQL Syntax]] 
  عشان كدا مصطلح ال NoSQL مش دقيق أوي لأني بستخدم فيها SQL بس عادي لسا بنستخدمه
- ال NoSQL (non-relational) بدأت تتشهر في آخر الشهر الماضي وبدأت تطور وبعدها بدأت تستبدل ال relational databases العادية 
- المفروض ال SW engineer يتعلم الاتنين عشان هيتعامل معاهم كتير
## Reference
When people talk about databases, they’re usually referring to **relational databases** (such as PostgreSQL, MySQL, Oracle, …); but there are many other kinds of databases used in the industry, which are globally referred to as **“NoSQL” databases**, even though they can be very different from each other, and serve very various purposes. Also, the name “NoSQL” comes from **SQL**, which is the name of the syntax used to give orders (CRUD operations, creating and deleting tables, …) to a relational databases; however, some non-relational databases, which are referred to as “NoSQL” give the option to use the SQL syntax. Therefore, the term “NoSQL” is quite controversial to refer to non-relational databases, but it is still widely used.

“NoSQL” (non-relational) databases have known a boost in popularity, over the last decade or so, so much that there was a point, a few years ago, where people were wondering if they were to replace relational databases entirely. But years later, the market has now solidified, NoSQL databases’ market share doesn’t progress much anymore and is now quite steady. The result: many NoSQL databases have made it into solid maturity, and are used in some very ambitious projects (as well as small ones), but relational databases are still by far the most used in projects, and are not going anywhere after all.

Therefore: it is crucial for a software engineer to know very well how relational databases work, because the odds are very strong that you will encounter them in your career; but it is also very important to get acquainted with the most popular types of NoSQL databases, because the odds that you run into them, however kinda smaller, are pretty strong too.