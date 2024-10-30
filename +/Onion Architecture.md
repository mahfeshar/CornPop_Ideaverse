قبل ما بنبدأ نشتغل بنحدد الـ **Architecture Pattern** اللي هنشتغل عليها وهنبني على أساسها الـ Application بتاعنا



بيبقا شبه البصلة عشان كدا إسمه Onion
بيبقا Scalable وممكن أخد Layer وأحطها في Project تاني من غير ما يحصل مشاكل وبرضو أسهل في التغيير والتيستينج 

الـ Domain Layer: بيكون جواها البروجكت كله بس not Implemented 
يعنى بيكون جواها ال Domain Model + كل Interfaces الموجودة

الـ Repository Layer: بيكون عبارة عن **Class Library** وبنشتغل فيها باتنين Design Patterns وهما: [[Generic Repository]] و 
ممكن يبقا عندي أكتر من Repository بسبب وجود أكتر من DbContext ووجود أكتر من DbContext بيبقا بسبب وجود أكتر من Database، عشان كدا بنحطها في الـ Repository
هنا الـ Contract موجود في الـ Domain Layer عشان لما يبقا عندي أكتر من Repository Layer كلهم يعملوا Implement لنفس الـ Interface بس كل واحدة بطريقتها فالـ Implementation مختلف بس نفس الـ Signature 

الـ Service Layer: بيبقا فيها كل الـ Services في مكان واحد عشان كدا احنا بنشتغل [[Monolithic]] مش [[Microservices]] لأن كلها DotNet في مكان واحد
والـ Contract بتاعها أو Interfaces موجودة في الـ Domain Layer
هنا هيعمل كل حاجة ليها علاقة بالـ **Business** يعني مثلًا الأوردر بيعدي على مراحل زي مثلًا إنه يبقا Draft وبعدين يتوافق عليه ويتبعت للشحن وهكذا

![[Pasted image 20241030085512.png]]

فالـ Solution اللي احنا عملناه هنعمل New project عبارة عن Class Library وهنسميه `Talabat.Core` ونمسح فايل الـ Class بتاعنا

ونعمل واحد كمان لل Repository Layer نسميه `Talabat.Repository` ونخليه Class Library

ونعمل واحد لل Service وهكذا

ممكن نزود حاجات تانية على حسب احتياجاتنا