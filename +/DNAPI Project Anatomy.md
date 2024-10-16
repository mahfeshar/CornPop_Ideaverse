
## 1. اختيار نوع المشروع - ASP.NET Core Web API  
لما تبدأ في **Visual Studio**، هنفتح "Create New Project" ونختار قالب **ASP.NET Core Web API**. 
القالب دا مخصص للـ backend، وبيخلينا نركز على بناء APIs من غير التعامل مع الواجهات الأمامية (front-end). 
لو مش لاقي القالب، ممكن تكتبه في البحث "Web API" وتختار النسخة المكتوبة بـ **C#**.

اختار أحدث نسخة من الـ **.NET Framework** وتأكد إنك مشغل الخيارات:
- الـ**Use Controllers**: مهم جدًا لأننا هنا هنعتمد على **Controller-based APIs**.  
- الـ**Enable OpenAPI Support**: دا اللي بيدينا **Swagger** عشان نقدر نعمل توثيق تلقائي للـ APIs.  
- الـ**Top-level Statements**: شيل العلامة منها عشان الكود يبان واضح بنمطه التقليدي (Class وNamespace).

## 2. Anatomy of the Project - فهم مكونات المشروع  
أول ملف مهم هو `Program.cs`. 
دا ملف البداية أو نقطة الدخول للمشروع، زي ما شفنا قبل كده في مشاريع الـ **Console Applications**، وبيحتوي على **Main Method**. 
ولكن في المشاريع الجديدة، لو استخدمت **Top-level Statements**، هتلاقي إنه اختصر كتابة الكود (من غير Namespace أو Class).

## ملف Program.cs

ملف `Program.cs` هو **نقطة البداية (Entry Point)** لأي مشروع ASP.NET Core. 
يتم استخدامه لتجهيز المشروع، إضافة الخدمات (Services)، وتحديد الـ Middleware الذي يتحكم في مسار الطلبات والردود.

#### **محتويات `Program.cs` :**

```csharp
var builder = WebApplication.CreateBuilder(args);

// إضافة الخدمات (Services) للـ Dependency Injection Container
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// تفعيل Swagger في بيئة التطوير فقط
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

// Middleware لتحويل الطلبات من HTTP إلى HTTPS
app.UseHttpsRedirection();

// Middleware للصلاحيات (Authorization)
app.UseAuthorization();

// ربط الـ Controllers بالـ Routes
app.MapControllers();

// تشغيل التطبيق
app.Run();
```

---

### 1. إعداد WebApplicationBuilder:
- **`WebApplication.CreateBuilder(args)`**:
  - يُنشئ **Builder Object** باستخدام **[[Builder Pattern]]**. 
  - هذا الـ Builder يتيح تجهيز التطبيق بإضافة الخدمات (مثل Controllers وSwagger) وضبط الإعدادات.

#### إضافة الخدمات (Services):
- **`builder.Services`**:
  - هو **Container** يتم فيه تعريف جميع الخدمات التي يمكن استخدامها في المشروع عبر **[[Dependency Injection]]**.  
  - الخدمات قد تكون من إطار العمل نفسه (مثل Controllers) أو من مكتبات خارجية (مثل أدوات التوثيق في Swagger).

- **`AddControllers()`**:  
  - يُضيف دعمًا لـ Controllers، وهي الجزء الأساسي الذي يحتوي على **Endpoints** الخاصة بـ API، حيث يتم تعريف جميع الإجراءات (Actions) التي تعالج الطلبات.

- **`AddEndpointsApiExplorer()`**:  
  - يُسهّل استكشاف الـ **Endpoints** في المشروع، خاصة في التطبيقات التي تستخدم **Minimal APIs**.
 - الـ **AddApiExplorer()**: عبارة عن أداة بتساعدك انك تشوف الـ API بتاعتك واللي الأبلكيشن بتاعك بيدعمها وبتبقا في البرامج اللي فيها Controllers 
- الـ **AddEndpointsApiExplorer()**: نفس اللي فوق بس دي عشان الـ minimal API 
- **`AddSwaggerGen()`**:  
  - يضيف دعمًا لتوليد الوثائق التلقائية باستخدام **Swagger**، مما يتيح للمطورين رؤية كل الـ Endpoints وتفاصيلها بشكل تفاعلي.

---

### 2. بناء التطبيق باستخدام `builder.Build()`
- بعد إضافة جميع الخدمات المطلوبة، نقوم باستخدام:
  ```csharp
  var app = builder.Build();
  ```
  لإنشاء **Web Application** جاهز لاستقبال الطلبات.

---

### 3. إعداد الـ Middleware:
الـ **Middleware** هو مجموعة من الأدوات التي تمر بها الطلبات (Requests) والاستجابات (Responses).  
- **`if (app.Environment.IsDevelopment())`**:  
  - يتم **تفعيل Swagger** وواجهة **SwaggerUI** في **بيئة التطوير فقط**، لضمان الأمان بعدم إتاحة التوثيق في بيئة الإنتاج.

  ```csharp
  if (app.Environment.IsDevelopment())
  {
      app.UseSwagger();
      app.UseSwaggerUI();
  }
  ```

- **`UseHttpsRedirection()`**:
  - يُعيد توجيه جميع الطلبات الواردة عبر HTTP إلى HTTPS لتعزيز الأمان.

- **`UseAuthorization()`**:
  - يضيف **Middleware** للتحقق من صلاحيات المستخدم. هذا لا يُفعّل الحماية مباشرة، بل يتطلب ضبط إعدادات **Authentication** و**Authorization** بشكل منفصل.

---

### 4. ربط الـ Controllers بالـ Routes:
- **`app.MapControllers()`**:
  - يقوم التطبيق تلقائيًا بالبحث عن جميع الـ **Controllers** الموجودة في المشروع وربطها بمسارات URL (Routes) بناءً على التعريفات في كل Controller.

---

### 5. تشغيل التطبيق:
- **`app.Run()`**:
  - يبدأ تشغيل التطبيق ويظل ينتظر استقبال الطلبات حتى يتم إيقافه. عند الوصول إلى هذا السطر، يبقى التطبيق في حالة تشغيل دائم إلى أن يتم إغلاقه.

---

### الهيكل العام للتدفق:
1. **إنشاء WebApplicationBuilder**: إعداد البيئة والخدمات.
2. **إضافة Middleware**: لتوجيه الطلبات والتحكم في الصلاحيات.
3. **ربط الـ Controllers**: تجهيز المسارات وربطها بالـ Endpoints.
4. **تشغيل التطبيق**: الانتظار حتى يتم استقبال الطلبات.

---
## 3. شرح بناء المشروع باستخدام WebApplicationBuilder  
في كود المشروع، بنستخدم `WebApplicationBuilder` اللي بيساعدنا نجهز **الـ Web Application** بالإعدادات والخدمات اللازمة (Services). 
الفكرة هنا إنه بيضيف الأدوات اللي بتسند المشروع عشان يشتغل بشكل صحيح، وده باستخدام **Dependency Injection**.

### **كود `Program.cs` الأساسي:**
```csharp
var builder = WebApplication.CreateBuilder(args);

// إضافة الخدمات (Services) للـ DI Container
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// تحديد الـ Middleware للتطوير
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();
app.UseAuthorization();

// ربط الـ Controllers بالـ Routes
app.MapControllers();

app.Run();
```

#### شرح الكود:
- الـ**WebApplication.CreateBuilder**: بنجهز المشروع ونضيف الخدمات اللي محتاجينها.
- الـ**Services**:  عبارة عن وعاء و**بحدد** من خلاله ايه هي الخدمات اللي هتكون متاحة في الأبلكيشن بتاعي بحيث أقدر أستعملها بعد كدا عن طريق الـ [[Dependency Injection]] وممكن الخدمات دي تبقا جاية من الـ .NET نفسه أو من خلال Third party libraries 
- الـ**AddControllers()**: بيدعم استخدام الـ Controllers في الـ API.
-
- الـ**AddSwaggerGen()**: بيوفر التولز لتوليد الوثائق باستخدام Swagger.
- الـ**UseHttpsRedirection()**: بيحول الطلبات إلى HTTPS عشان الأمان.
- الـ**UseAuthorization()**: بيضيف الـ Middleware الخاص بالصلاحيات.
- الـ**MapControllers()**: بيربط الـ Controllers بالـ Routes الخاصة بيهم.

## 4. الـ Controllers وأهميتهم في المشروع  
في المشاريع اللي بتستخدم **ASP.NET Core Web API**، بننظم الكود في **Controllers**، وكل Controller بيكون مسؤول عن مجموعة من الوظائف. مثال: ممكن يكون عندنا **StudentController** لإدارة بيانات الطلاب، و**EmployeeController** لإدارة بيانات الموظفين.

#### **WeatherForecastController.cs - Controller Sample:**
```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    private static readonly string[] Summaries = new[]
    {
        "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
    };

    [HttpGet(Name = "GetWeatherForecast")]
    public IEnumerable<WeatherForecast> Get()
    {
        return Enumerable.Range(1, 5).Select(index => new WeatherForecast
        {
            Date = DateTime.Now.AddDays(index),
            TemperatureC = Random.Shared.Next(-20, 55),
            Summary = Summaries[Random.Shared.Next(Summaries.Length)]
        })
        .ToArray();
    }
}
```

#### شرح الكود:
- **[ApiController]**: بيعلم إن الكلاس دا API Controller.
- **[Route("[controller]")]**: بيوفر Routing ديناميكي باستخدام اسم الـ Controller.
- **[HttpGet]**: بيعرف إن الميثود دي بتستجيب لطلبات HTTP GET.

الميثود `Get()` بترجع مجموعة من بيانات الطقس بشكل عشوائي باستخدام **IEnumerable**. 

### 5. فهم Swagger UI واستخدامه في المشروع  
**Swagger** هو أداة قوية بتساعد في توثيق واختبار الـ APIs بشكل تلقائي. لما نشغل المشروع باستخدام **Swagger UI**، هيفتح متصفح بـ واجهة سهلة نقدر منها نستعرض الـ API ونجربها.

#### **Swagger في وضع التشغيل:**
لما نشغل التطبيق ونفتح **Swagger UI**، هنشوف الـ Endpoints المتاحة مع وصف ليهم. بنقدر نضغط على أي Endpoint ونجربه باستخدام **Try it out** عشان نختبر الـ API مباشرة من الواجهة.

### 6. ملاحظات حول الأمان والاستخدام في بيئات مختلفة  
- **Swagger** بيتفعل في بيئة التطوير فقط (**Development Environment**). في الإنتاج (**Production**)، بنقفل الـ Swagger لأسباب أمان، عشان ما نديش أي معلومات حساسة عن الـ APIs.
- ممكن نفعّله في أنظمة داخلية لو الشبكة مغلقة، عشان يسهل على الفرق المختلفة التواصل مع الـ APIs.

### 7. ملفات إعدادات المشروع - appsettings.json  
الملف `appsettings.json` بيحتوي على إعدادات المشروع زي الـ **Connection Strings** للداتابيس، مفاتيح التشفير، وأي بيانات تانية بتتغير حسب البيئة (زي التطوير، الاختبار، أو الإنتاج).

### 8. أهمية Postman في اختبار الـ APIs  
إلى جانب **Swagger**، هنحتاج نستخدم **Postman**. دي أداة من Google بتمكننا من اختبار الـ APIs بطرق متقدمة، وإرسال طلبات معقدة (GET, POST, PUT, DELETE) وتجربة ردود الأفعال المختلفة.

---

### الخاتمة  
الفيديو دا غطى الأساسيات المهمة في بناء مشروع **ASP.NET Core Web API**، من إنشاء المشروع، إعداد `Program.cs`، تنظيم الـ Controllers، لاستخدام Swagger. في الحلقات الجاية، هنتعمق أكتر في بناء الـ APIs ونشرح الميدل وير بالتفصيل. استعد للتطبيق العملي باستخدام **Postman** وتجربة السيناريوهات المختلفة!

**اشوفكم في فيديو جديد قريب، والسلام عليكم ورحمة الله وبركاته!**