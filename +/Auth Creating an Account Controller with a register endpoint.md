---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-15
---
هنتكلم عن إضافة خاصية تسجيل المستخدمين للتطبيق، وده جزء أساسي في أي تطبيق بيحتوي على مستخدمين، زي تطبيقات السوشيال ميديا أو التطبيقات اللي بتحتاج لتسجيل دخول المستخدمين. 
عشان نعمل الخاصية دي، هنستخدم **Controller** جديد في الـ API ونضيف وظائف لتسجيل المستخدمين الجدد.

### 1. إنشاء Accounts Controller:
أول حاجة بنعملها هي إنشاء **controller** جديد باسم **`AccountsController`**. الكود الأساسي هنا بيكون مشابه لأي **controller** آخر، لكن بدلاً من إعادة كتابة كل شيء من الصفر، بنرث (derive) الـ **controller** الجديد من **`BaseApiController`** اللي عملناه قبل كده، وده بيساعد في تقليل التكرار في الكود.

```csharp
public class AccountsController : BaseApiController
{
    private readonly DataContext _context;

    public AccountsController(DataContext context)
    {
        _context = context;
    }
}
```

### 2. إضافة Endpoint لتسجيل المستخدم:
الخطوة الجاية هي إضافة **endpoint** جديد لتسجيل المستخدمين. 
هنستخدم **HTTP POST** لأننا هنرسل بيانات من المستخدم (زي اسم المستخدم وكلمة المرور) إلى السيرفر. 
الـ **endpoint** هتكون بالشكل ده:

```csharp
[HttpPost("register")]
public async Task<ActionResult<AppUser>> Register(string username, string password)
{
    using var hmac = new HMACSHA512(); // Salt
    
    var user = new AppUser
    {
        Username = username,
        PasswordHash = hmac.ComputeHash(Encoding.UTF8.GetBytes(password)),
        PasswordSalt = hmac.Key
    };

    _context.Users.Add(user);
    await _context.SaveChangesAsync();

    return user;
}
```

### 3. مفهوم HMACSHA512 والـ Password Hashing:
تم استخدام **HMACSHA512** لتشفير كلمة المرور الخاصة بالمستخدم. 
ببساطة، التشفير ده بيحول كلمة المرور لنص مشفر (hash)، وده بيساعد في حماية كلمة المرور بشكل أكبر لأن حتى لو قاعدة البيانات تم اختراقها، الهكرز مش هيقدروا يرجعوا لكلمة المرور الأصلية بسهولة.

- **Password Hash**: ده عبارة عن تحويل كلمة المرور لصيغة غير قابلة للإرجاع باستخدام خوارزمية تشفير.
- **Password Salt**: ده جزء عشوائي بيتم إضافته لعملية التشفير عشان نخلي كل كلمة مرور فريدة حتى لو المستخدمين استخدموا نفس كلمة المرور.

اتكلمنا عنها في [[Auth Safe storage of passwords]]

### Using statement
عندنا حاجة اسمها [[Cs Value and Reference Types#Garbage Collector|Garbage collector]]
### 4. التعامل مع الـ DataContext:
في الكود، بنضيف المستخدم الجديد لقائمة المستخدمين في قاعدة البيانات باستخدام **Entity Framework**، اللي بتساعد في التعامل مع البيانات بشكل سلس في التطبيقات.

```csharp
_context.Users.Add(user);
await _context.SaveChangesAsync();
```

### 5. اختبار الـ API باستخدام Postman:
بعد ما بنضيف الكود، لازم نختبر هل الـ **API** شغالة بشكل صحيح. في الفيديو، بنستخدم **Postman** لإرسال طلبات HTTP لـ **API**. بيتم إرسال طلب لتسجيل مستخدم جديد باستخدام الـ **POST**، وبيتم إرسال اسم المستخدم وكلمة المرور في الطلب. 

لكن حصلت مشكلة في البداية بسبب طريقة إرسال البيانات، حيث كانت البيانات بتتبعت في جسم الطلب (body) لكن الـ **API** مش قادرة تربط بين البيانات اللي في الجسم والـ **parameters** في الكود.

### 6. الحل:
الفيديو وضح إن الحل الأمثل هو إرسال البيانات كـ **query string** (يعني في رابط الـ URL). وبالتالي بعد التعديل، بقى الطلب كالتالي:

```http
api/account/register?username=sam&password=password
```

وده اشتغل بشكل صحيح، وتم إنشاء المستخدم بنجاح.

### 7. التحليل باستخدام الـ Debugger:
الفيديو وعد بشرح كيفية استخدام الـ **Debugger** في الخطوة الجاية عشان نفهم أكتر المشاكل اللي بتحصل وقت معالجة الطلبات في السيرفر، ودي هتساعدنا في اكتشاف الأخطاء وتعديلها بشكل أسرع.

### خلاصة:
في الفيديو ده، تم شرح كيفية إضافة خاصية تسجيل المستخدمين في التطبيق باستخدام **AccountsController** والاعتماد على **HMACSHA512** لتشفير كلمات المرور وحمايتها. وتم شرح استخدام **Postman** لاختبار الـ **API** وكيفية التعامل مع المشكلات اللي ممكن تواجهك في الربط بين البيانات اللي في الطلبات والـ **API** نفسها.