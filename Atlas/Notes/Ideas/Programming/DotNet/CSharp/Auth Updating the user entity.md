---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-15
---
إعداد نظام لكلمات المرور وتسجيل الدخول في تطبيقنا، وهنبدأ بخطوات بسيطة عشان نوضح الأساسيات. 
## مقدمة عن إعداد نظام كلمة المرور وتسجيل الدخول
أول حاجة بيتم توضيحها هي كيفية إعداد الـ **password** system في التطبيق اللي بنبنيه. التطبيق ده بيسمح للمستخدمين بتسجيل الدخول، وهنقوم بتخزين معلومات كلمات المرور بشكل آمن في قاعدة البيانات. 

### مشكلة الـ Hot Reload:
قبل ما ندخل في تفاصيل تخزين كلمة المرور،هنعاني من مشكلة في ميزة اسمها **Hot Reload**، اللي بتتيح تحديث التطبيق بدون الحاجة لإعادة تشغيله بالكامل. 
لكن الميزة دي، في حالته، مش بتشتغل بشكل صحيح وبتؤدي إلى تحديثات مضللة في الكود، وده ممكن يسبب مشاكل أثناء تطوير التطبيق.

فـ هو قرر يعطل الـ **Hot Reload** باستخدام أمر في الـ **.NET CLI** عشان يتجنب المشاكل دي. الطريقة اللي استخدمها هي إنه شغل التطبيق بأمر:
```bash
dotnet watch --no-hot-reload
```

### إضافة خصائص لكائن المستخدم:
هنعمل إضافة خصائص جديدة لكائن المستخدم (User entity) عشان نقدر نخزن معلومات كلمة المرور. 
الكلمات المرور بتتخزن كـ **byte arrays** في قاعدة البيانات، واحدة للـ **Password Hash** والثانية للـ **Password Salt**.

الكود المستخدم لإضافة الخصائص دي:
```csharp
public class User
{
    public int Id { get; set; }
    public string Username { get; set; }
    public byte[] PasswordHash { get; set; }
    public byte[] PasswordSalt { get; set; }
}
```

### التحديثات في قاعدة البيانات:
بعد ما ضفنا الخصائص دي لكائن المستخدم، محتاجين نقول لقاعدة البيانات إنها تضيف أعمدة جديدة تتوافق مع الخصائص اللي ضفناها. 
بنعمل ده عن طريق **Migration** جديدة.

أمر إنشاء الـ **Migration**:
```bash
dotnet ef migrations add UserPasswordAdded
```

وبعد كده بنستخدم الأمر ده لتحديث قاعدة البيانات:
```bash
dotnet ef database update
```

### دور [[Entity Framework]]:
في الحالة دي، إحنا بنستخدم **SQLite**، والـ **Entity Framework** بترجم الـ **byte arrays** لصيغة اسمها **BLOB** (Binary Large Object) في قاعدة البيانات. 
وده اللي بيحصل تلقائيًا من غير تدخلنا.

### مراجعة قاعدة البيانات:
بعد تحديث قاعدة البيانات، نقدر نراجع التغييرات دي من خلال فتح قاعدة البيانات باستخدام **SQLite**، وهنلاقي الأعمدة الجديدة للـ **Password Hash** و **Password Salt** موجودة لكن قيمها فاضية لأننا لسه ما دخلناش أي بيانات.

### ختام الفيديو:
الجزء الأخير في الفيديو بيشاور إن في الدرس اللي جاي هيتم شرح كيفية إنشاء **Base API Controller** واستخدام **Inheritance** لتقليل التكرار في الكود.

### خلاصة:
في الفيديو ده، الهدف الأساسي كان إعداد نظام لتخزين كلمات المرور بشكل آمن باستخدام الـ **Password Hashing** و **Salting** في C#. وتم شرح أهمية تعطيل ميزة الـ **Hot Reload** بسبب المشاكل اللي بتسببها خلال التطوير، وأخيرًا تم توضيح كيفية تحديث قاعدة البيانات باستخدام **Entity Framework** لإنشاء الأعمدة المطلوبة لتخزين كلمات المرور بشكل آمن.