قبل ما بنبدأ نشتغل بنحدد الـ **Architecture Pattern** اللي هنشتغل عليها وهنبني على أساسها الـ Application بتاعنا

بيبقا شبه البصلة عشان كدا إسمه Onion
الـ Domain Layer: بيكون جواها البروجكت كله بس not Implemented 
يعنى بيكون جواها ال Domain Model + كل Interfaces الموجودة

الـ Repository Layer: بيكون عبارة عن **Class Library** وبنشتغل فيها باتنين Design Patterns وهما: [[Generic Repository]] و 
ممكن يبقا عندي أكتر من Repository بسبب وجود أكتر من DbContext ووجود أكتر من DbContext بيبقا بسبب وجود أكتر من Database