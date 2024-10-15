---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-15
---
الشرح بيتمحور حول إزاي نتجنب تكرار الكود في التطبيق اللي بنبنيه، وخصوصًا في التعامل مع **API controllers**. 
الفكرة الأساسية هي إننا لو عندنا أكتر من **controller** في التطبيق، مش لازم نكتب نفس الأكواد في كل **controller**، بل ممكن نستفيد من خاصية الـ **[[Cs Inheritance]]** في C# عشان نقلل التكرار ده.

### مشكلة تكرار الكود في الـ Controllers
كل **API controller** بيحتاج حاجات مشتركة زي:
1. **API controller attribute**.
2. الـ**Route** لتحديد المسار اللي الـ API هيستقبل عليه الطلبات.
3. كل **controller** لازم يرث من الـ **ControllerBase** class.

بدل ما نكتب الحاجات دي في كل **controller**، ممكن نعمل **Base API controller** يرث منه باقي الـ **controllers**. 
ده بيساعدنا على تقليل تكرار الكود ويخلي التطبيق أسهل في الصيانة. [[DRY]]

### إنشاء Base API Controller
الخطوة الأولى هي إنشاء كلاس جديد في مجلد **Controllers** باسم `BaseApiController`، والكود اللي بنكتبه فيه هو:

```csharp
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class BaseApiController : ControllerBase
{
}
```

الفكرة هنا إننا بنحط **attributes** اللي بنحتاجها في كل **controller** زي **`ApiController`** و **Route**. 
بعد كده، بدل ما يرث كل **controller** من **`ControllerBase`**، بنخليه يرث من **`BaseApiController`**، وبكده نبقى اتجنبنا كتابة نفس الحاجات في كل **controller**.

### تعديل الـ UsersController
في الخطوة التالية، هنعمل تعديل في الـ **`UsersController`** عشان يرث من الـ **`BaseApiController`** بدل **`ControllerBase`**. 
الكود هيبقى بالشكل ده:

```csharp
public class UsersController : BaseApiController
{
    // باقي الأكواد الخاصة بالـ UsersController
}
```

### اختبار التغييرات باستخدام Postman
بعد ما عملنا التغييرات دي، لازم نختبر هل الـ **API** شغال بشكل صحيح ولا لأ. 
الفيديو شرح إزاي نستخدم **Postman** لاختبار نقاط النهاية (endpoints) بتاعت الـ **API**.
موجود في الفايل وهتعمله Import بس

**Postman** هو أداة بتسمحلك تبعت طلبات HTTP للـ **API** وتستقبل الردود عشان تتأكد إن كل حاجة شغالة بشكل صحيح. بدل ما نكتب كل طلب يدويًا كل مرة، الفيديو وضح إننا ممكن نستخدم مجموعة طلبات جاهزة (Postman collection) لتسريع عملية الاختبار.

### اختبار WeatherForecastController و UsersController
أول حاجة اختبرها هي **`WeatherForecastController`** بعد ما عدل الكود عشان يرث من **`BaseApiController`**. 
طلب منه يعمل طلب لـ **API** باستخدام المسار الجديد:

```http
api/weatherforecast
```

والرد اللي استلمه كان قائمة ملخصات الطقس.

بعد كده اختبر **`UsersController`** وبعت طلب لـ:

```http
api/users
```

والرد اللي استلمه كان بيانات المستخدمين في قاعدة البيانات، بما فيها أعمدة **PasswordHash** و **PasswordSalt** اللي أضفناها سابقًا.

### استخدام Postman في تسريع الاختبار
الفيديو وضح كمان إن **Postman** بيتيحلك إنشاء وتخزين طلبات HTTP، وده بيخلي عملية الاختبار أسرع وأسهل. 
بدل ما تكتب الطلبات يدويًا كل مرة، ممكن تحفظها وتعيد استخدامها.