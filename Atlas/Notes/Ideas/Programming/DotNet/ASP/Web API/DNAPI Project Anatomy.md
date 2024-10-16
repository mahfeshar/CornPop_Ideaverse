---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-10-16
---

## 1. Make Project Web API  
لما تبدأ في **Visual Studio**، هنفتح "Create New Project" ونختار قالب **ASP.NET Core Web API**. 
القالب دا مخصص للـ backend، وبيخلينا نركز على بناء APIs من غير التعامل مع الواجهات الأمامية (front-end). 
لو مش لاقي القالب، ممكن تكتبه في البحث "Web API" وتختار النسخة المكتوبة بـ **C#**.

اختار أحدث نسخة من الـ **.NET Framework** وتأكد إنك مشغل الخيارات:
- الـ**Use Controllers**: مهم جدًا لأننا هنا هنعتمد على **Controller-based APIs**.  
- الـ**Enable OpenAPI Support**: دا اللي بيدينا **Swagger** عشان نقدر نعمل توثيق تلقائي للـ APIs.  
- الـ**Top-level Statements**: شيل العلامة منها عشان الكود يبان واضح بنمطه التقليدي (Class وNamespace).

## 2. Anatomy of the Project  
أول ملف مهم هو `Program.cs`. 
دا ملف البداية أو نقطة الدخول للمشروع، زي ما شفنا قبل كده في مشاريع الـ **Console Applications**، وبيحتوي على **Main Method**. 
ولكن في المشاريع الجديدة، لو استخدمت **Top-level Statements**، هتلاقي إنه اختصر كتابة الكود (من غير Namespace أو Class).

## 3. Program.cs file

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
  - يبدأ تشغيل التطبيق ويظل ينتظر استقبال الطلبات حتى يتم إيقافه. 
  - عند الوصول إلى هذا السطر، يبقى التطبيق في حالة تشغيل دائم إلى أن يتم إغلاقه.

---

### الهيكل العام للتدفق:
1. **إنشاء WebApplicationBuilder**: إعداد البيئة والخدمات.
2. **إضافة Middleware**: لتوجيه الطلبات والتحكم في الصلاحيات.
3. **ربط الـ Controllers**: تجهيز المسارات وربطها بالـ Endpoints.
4. **تشغيل التطبيق**: الانتظار حتى يتم استقبال الطلبات.

---
## 4. Controllers
في المشاريع اللي بتستخدم **ASP.NET Core Web API**، بننظم الكود في **Controllers**، وكل Controller بيكون مسؤول عن مجموعة من الوظائف. 
الـ **Controller** هو مكون أساسي يحتوي على **الإجراءات (Actions)** التي يتم الوصول إليها عبر طلبات HTTP (مثل GET، POST، PUT).
كل Controller يمثل مجموعة من **Endpoints** ذات علاقة ببعضها.
مثال: ممكن يكون عندنا **StudentController** لإدارة بيانات الطلاب، و**EmployeeController** لإدارة بيانات الموظفين.

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

- الـ`ApiController`: **بيعلم** إن الكلاس دا API Controller.
  كلمة `ApiController` دي بنقول عليها Attribute أو Decoration لأنها بتخلي الـ Function يغير الديكور بتاعه ويعمل حاجات مكنش بيعملها، واستعملنا واحدة زيها قبل كدا في الـ [[Cs Enums]] وهي مشروحه في الـ [[Reflection]]
- الـ`[Route("[controller]")]`: بيوفر Routing ديناميكي باستخدام اسم الـ Controller.
  الـ Controller دا لما هاجي أوصله من خلال الـ URL بتاعه هيكون شكله عامل إزاي
  كلمة controller بين ال Square bracket دا معناه ان الـ URL هيبقا كدا `https://myapp.com/ClassName`
- الـ`[HttpGet]`: بيعرف إن الميثود دي بتستجيب لطلبات HTTP GET.

الميثود `Get()` بترجع مجموعة من بيانات الطقس بشكل عشوائي باستخدام **[[Cs Enumerable|IEnumerable]]**. 
### الفرق في الوراثة بين MVC و API:
- في الـ **MVC**:
  - الـ Controller بيورث من **Controller** class وهو بيبقا وارث من الـ `BaseController`.
  - بيورث من كلاس وارث ليه؟ 
    بيكون عنده حاجات إضافية زي **`ViewData`** و`TempData` اللي بتتعامل مع البيانات قبل ما توصل للمستخدم.

- في الـ **API**:
  - الـ Controller بيورث من **`BaseController`** على طول.
  - مش بيحتاج أي `ViewData` أو `TempData` لأنه مش بيرجع بيانات كـ View.

### Routes for Endpoints
#### **1. تعريف الـ Default Route**
عند إنشاء **API Controller** يحتوي على **GET Endpoint**، إذا لم يتم تحديد **Route مخصص** لهذا الـ Endpoint، سيقوم التطبيق باستخدام **المسار الافتراضي** للوصول إليه. 
يتم تحديد هذا المسار من خلال **اسم Controller واسم Action Method**.


```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    [HttpGet]
    public IEnumerable<WeatherForecast> Get()
    {
        return new List<WeatherForecast>
        {
            new WeatherForecast { Date = DateTime.Now, TemperatureC = 25, Summary = "Sunny" }
        };
    }
}
```
- **Default Route** سيكون بالشكل التالي:

```
https://localhost:5001/WeatherForecast
```

- هنا:
  - الـ`WeatherForecast` هو **اسم Controller** (بدون كلمة "Controller" في النهاية).
  - **الطلب GET** سيصل إلى الـ **Action Method** المسماة `Get()` تلقائيًا لأنه لم يتم تحديد **Route** خاص بها.

---

#### **2. تحديد Route مخصص للـ Endpoint**
يمكنك تحديد **Route مخصص** لأي Endpoint باستخدام **Attributes** مثل `[HttpGet]` مع إضافة **Route** إلى الـ **Method** نفسها.
```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    [HttpGet("get-weather")]
    public IEnumerable<WeatherForecast> GetWeather()
    {
        return new List<WeatherForecast>
        {
            new WeatherForecast { Date = DateTime.Now, TemperatureC = 25, Summary = "Cloudy" }
        };
    }
}
```

- في هذه الحالة، سيكون المسار المخصص هو:

```
https://localhost:5001/WeatherForecast/get-weather
```

- **الفرق هنا**: يجب على المستخدم كتابة `/get-weather` للوصول إلى هذا الـ Endpoint.

#### **3. الوصول بدون Route مخصص (Default Action)**
إذا لم يتم تحديد **Route** لأي Method أخرى، يتم التعامل مع أول **GET Method** على أنها الـ **Default GET Method**. 
أي طلب يتم إرساله إلى الـ **Controller** نفسه (بدون تحديد أي Action Method) سيتم توجيهه إلى هذه **Method**.

```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    [HttpGet]
    public IEnumerable<WeatherForecast> Get()
    {
        return new List<WeatherForecast>
        {
            new WeatherForecast { Date = DateTime.Now, TemperatureC = 28, Summary = "Rainy" }
        };
    }

    [HttpGet("detailed")]
    public IEnumerable<WeatherForecast> GetDetailed()
    {
        return new List<WeatherForecast>
        {
            new WeatherForecast { Date = DateTime.Now, TemperatureC = 28, Summary = "Heavy Rain" }
        };
    }
}
```
- للوصول إلى **Default GET Method**:

```
https://localhost:5001/WeatherForecast
```

- للوصول إلى **Method مخصصة** (`GetDetailed`):

```
https://localhost:5001/WeatherForecast/detailed
```

---

يمكنك أيضًا تمرير **Parameters** في الـ Route، مثل **ID أو تاريخ**، للوصول إلى بيانات معينة.

#### **مثال: Route مع Parameter**

```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    [HttpGet("{date}")]
    public WeatherForecast GetByDate(DateTime date)
    {
        return new WeatherForecast { Date = date, TemperatureC = 30, Summary = "Windy" };
    }
}
```

- يمكن الوصول إلى هذه الـ Method بتمرير **تاريخ** كـ Parameter:

```
https://localhost:5001/WeatherForecast/2024-10-16
```

- في هذا المثال:
  - يتم تمرير `2024-10-16` كـ **Parameter** إلى الـ Method `GetByDate`.

#### **5. استخدام Query Parameters في URL**
يمكن أيضًا استخدام **Query Parameters** بدلاً من وضع الـ Parameters في المسار نفسه.

```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    [HttpGet]
    public WeatherForecast GetByQuery([FromQuery] string city)
    {
        return new WeatherForecast { Date = DateTime.Now, TemperatureC = 35, Summary = $"Weather in {city}" };
    }
}
```

- باستخدام **Query Parameter**:

```
https://localhost:5001/WeatherForecast?city=Cairo
```


#### **6. تلخيص الطرق المختلفة للوصول إلى الـ GET Endpoints:**
1. الـ**Default Route بدون تخصيص**:
   - `https://localhost:5001/WeatherForecast`
   - يتم الوصول إلى أول **GET Method** بشكل افتراضي.

2. الـ**Route مخصص باستخدام Attribute**:
   - `https://localhost:5001/WeatherForecast/get-weather`
   - يتم تحديد المسار داخل `[HttpGet("route-name")]`.

3. الـ**Route مع Parameters في URL**:
   - `https://localhost:5001/WeatherForecast/2024-10-16`
   - يتم تمرير الـ Parameters في المسار مباشرةً.

4. الـ**Query Parameters في URL**:
   - `https://localhost:5001/WeatherForecast?city=Cairo`
   - يتم تمرير الـ Parameters باستخدام Query String.
## 5. appsettings.json  
الـ `appsettings.json` هو ملف مهم جدًا في مشاريع الـ ASP.NET Core لأنه بيخزن إعدادات التكوين (configuration settings) اللي بيستخدمها التطبيق. 
الملف ده بيوفر طريقة مرنة لتغيير الإعدادات زي الـ Connection Strings الخاصة بالـ Database أو أي إعدادات تانية من غير ما نحتاج نعدل في الكود مباشرة. 
وده بيكون مفيد جدًا لما نيجي ننقل التطبيق بين بيئات مختلفة (زي بيئة التطوير أو الإنتاج).

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=StoreDB;Trusted_Connection=True;"
  }
}
```

- الـ**Logging**:
  - ده الجزء الخاص بإعدادات الـ Logging (يعني إزاي التطبيق بيسجل الأحداث اللي بتحصل أثناء التشغيل).
  - ممكن تحدد مستوى الـ Logging لكل نوع (مثلاً: **Information**، **Warning**، أو **Error**). في المثال ده، المستوى الافتراضي هو **Information** (يعني هيسجل كل الأحداث المعلوماتية)، وبالنسبة لأحداث الـ **`Microsoft.AspNetCore`** هيسجل **Warning** فقط.

- الـ`AllowedHosts`:
  - ده اللي بيسمح لك تحدد الـ Hosts اللي التطبيق ممكن يتفاعل معاها. لو كتبت "\*" ده معناه إن التطبيق ممكن يتفاعل مع أي Host.

- الـ`ConnectionStrings`:
  - هنا بنحط الـ Connection Strings الخاصة بالـ Database. في المثال ده، بنستخدم **SQL Server** المحلي (`LocalDB`) والـ Database اسمها **`StoreDB`**.
  - الـ Connection String دي بتقول للتطبيق يتصل بـ SQL Server ويستخدم `StoreDB` كقاعدة بيانات.

## 6. launchSettings.json:

```json
{
  "$schema": "http://json.schemastore.org/launchsettings.json",
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:48931",
      "sslPort": 44327
    }
  },
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "launchUrl": "swagger",
      "applicationUrl": "http://localhost:5055",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "launchUrl": "swagger",
      "applicationUrl": "https://localhost:7078;http://localhost:5055",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "launchUrl": "swagger",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

- الـ**iisSettings**:  
  - بيعطل **Windows Authentication** ويسمح بالـ **Anonymous Access**.
  - الـ IIS Express شغال على `http://localhost:48931` بـ SSL Port `44327`.

- الـ**profiles**: عندك 3 بروفايلات لتشغيل المشروع:
  دي عبارة عن الـ Servers اللي تقدر تشغل بيها عندك
  1. الـ**http**: تشغيل المشروع على **HTTP** باستخدام **Kestrel** على `http://localhost:5055`.
  2. الـ**https**: تشغيل المشروع على **HTTPS** و**HTTP** معًا على `https://localhost:7078` و `http://localhost:5055`.
  3. الـ**IIS Express**: بيشغل المشروع على IIS Express مع توثيق **Swagger**.

- كل البروفايلات بتستخدم بيئة **Development** وبتفتح الـ **Swagger** تلقائيًا بعد التشغيل.


## 5. Swagger UI  
الـ**Swagger** هو أداة قوية بتساعد في توثيق واختبار الـ APIs بشكل تلقائي. 
لما نشغل المشروع باستخدام **Swagger UI**، هيفتح متصفح بـ واجهة سهلة نقدر منها نستعرض الـ API ونجربها.

![[Pasted image 20241016235142.png]]
![[Pasted image 20241016235304.png]]

## 6. ملاحظات حول الأمان والاستخدام في بيئات مختلفة  
- الـ**Swagger** بيتفعل في بيئة التطوير فقط (**Development Environment**). 
- في الإنتاج (**Production**)، بنقفل الـ Swagger لأسباب أمان، عشان ما نديش أي معلومات حساسة عن الـ APIs.
- ممكن نفعّله في أنظمة داخلية لو الشبكة مغلقة، عشان يسهل على الفرق المختلفة التواصل مع الـ APIs.

## 7. أهمية Postman في اختبار الـ APIs  
إلى جانب **Swagger**، هنحتاج نستخدم **Postman**. 
دي أداة من Google بتمكننا من اختبار الـ APIs بطرق متقدمة، وإرسال طلبات معقدة (GET, POST, PUT, DELETE) وتجربة ردود الأفعال المختلفة.

