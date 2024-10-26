---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-10-26
---
## الفرق بين MVC والـ API:
- في الـ **MVC**:
  - لما الـ user يبعت request للـ MVC، التطبيق بيرجع **View** فيه البيانات المطلوبة ويظهرها للمستخدم.
  - الـ View ده بيكون مليان بالبيانات اللي جايه من الـ Controller.

- في الـ **API**:
  - الـ API مش بترجع Views، هي بترجع البيانات في شكل **JSON**.
  - الـ JSON ده بيتبعت للـ Frontend Developer وهو اللي يعرض البيانات عنده على الصفحة أو الواجهة بتاعته.

## Onion Architecture
- بنشتغل هنا بالـ **Onion Architecture** اللي بتنظم طريقة تقسيم المشروع بشكل يسهل صيانته وتعديله.

## خطوات إنشاء Project API:

![[Pasted image 20241016045609.png]]
### 1. Create New Project:
- تفتح Visual Studio وتختار "Create New Project".
- تختار نوع المشروع "ASP.NET Core Web API".
- تكتب اسم المشروع وتختار مكانه.
- تختار النسخة **.NET 8** .

### 2. Use Controller:
- لو شلت علامة الصح من خيار "Use Controller"، المشروع هيبقى من غير Controllers زي اللي بنشوفه في **Node.js**، وده مش الطريقة المعتادة.

### 3. Enable OpenAPI:
- الـ**OpenAPI** هو بلجن بيعمل documentation أو توثيق للـ API اللي انت بتبنيها، وده بيكون مفيد جدًا لتسهيل التعامل مع الـ API من خلال أدوات زي **Postman**.
  اللي هي الـ Swagger باختصار
## Structure المشروع (Folder Structure):
- هتلاقي فولدر اسمه **Controllers**، وده اللي بيكون فيه كل الكلاسات اللي هتتعامل مع الـ HTTP requests والـ responses.
- كل Controller بيكون جواه Route خاص بيه بالشكل ده:
  ```csharp
  [Route("[controller]")]
  [ApiController]
  ```
  هنا بنحدد اسم الكنترولر اللي هيتعامل مع الـ requests من خلال اسم الـ controller في الـ route.
## استخدام Postman واختبار الـ API:
- بعد تشغيل المشروع، بتفتح **Postman** وتضيف الـ URL الخاص بالـ API (اللي بيكون عادةً **localhost**).
- بتعمل Request لكل Endpoint عشان تجرب الـ API.
- تقدر تعمل **Export** للـ Collection من Postman عشان تبعته لأي حد يشتغل معاك على المشروع.

## RESTful APIs:
- الـ REST API بتشتغل على أساس الـ HTTP Verbs زي **GET**، **POST**، **PUT**، و**DELETE**.
- مثلاً، لو بعت **GET** request، الـ API هيرد بالبيانات، ولو بعت **POST** هيضيف البيانات.

## مميزات .NET 6 و .NET 8:
- في .NET 6 تم دمج ملفات الـ `Program` و `Startup` في ملف واحد لتبسيط الكود.
- في .NET 8، التحسينات بتركز أكتر على الأداء وزيادة دعم مميزات زي الـ **Blazor** والـ **Minimal APIs**، بالإضافة إلى تحسينات كبيرة في سرعة الاستجابة وتطوير الأدوات الخاصة بالـ Developer Experience.

## مثال على استخدام الـ Dependency Injection مع الـ`DbContext`:
- هنا بنستخدم SQL Server كـ Database للـ API:
  ```csharp
  builder.Services.AddDbContext<StoreContext>(options => {
      options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"));
  });
  ```
  - الـ Dependency Injection هنا بتمكننا من استدعاء الـ DbContext بسهولة في أي مكان في الكود.


## شرح dummy example:

في بداية أي مشروع ASP.NET Core Web API، بيجي معاه **dummy example** بيبسط مفهوم الـ API عن طريق تقديم مثال بسيط اسمه **`WeatherForecast`**. 
ده عبارة عن كلاس بيستخدمه المشروع عشان يرجع بيانات وهمية (dummy data) عن درجات الحرارة المتوقعة، وده بيسهل فهم إزاي الـ API شغالة.

#### Class
```csharp
public class WeatherForecast
{
    public DateTime Date { get; set; }  // تاريخ اليوم
    public int TemperatureC { get; set; }  // درجة الحرارة بالـ Celsius
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);  // حساب درجة الحرارة بالـ Fahrenheit
    public string? Summary { get; set; }  // وصف الطقس (مشمس، ممطر، إلخ)
}
```

#### الـController بتاع `WeatherForecast`:

الكلاس ده بيستخدمه الـ API في **`WeatherForecastController`**. 
ده الـ Controller اللي بيستقبل الـ HTTP requests وبيعمل Generate للـ Weather data الوهمية ويرجعها كـ JSON.

```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    private static readonly string[] Summaries = new[]
    {
        "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
    };

    [HttpGet]
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

- الـ**Summaries**: مصفوفة فيها بعض الأوصاف لحالة الطقس (مثلاً "Freezing" يعني برد جامد، "Hot" يعني حر جدًا، إلخ).
- الـ`HttpGet`: ده الـ Action اللي بيتم استدعاؤه لما نبعت request على الـ route بتاع الـ Controller (اللي هو "`WeatherForecast`" في الحالة دي).
- الـ**Get()**: بتعمل Loop على عدد الأيام (من 1 لـ 5 أيام قدام) وبتعمل Generate لبيانات الطقس الوهمية.
  - الـ**Date**: بيحسب تاريخ الأيام الجاية.
  - الـ**TemperatureC**: بيستخدم Random عشان يجيب درجة حرارة عشوائية بين -20 و 55.
  - الـ**Summary**: بيجيب وصف عشوائي للطقس من مصفوفة **Summaries**.

#### النتيجة:
لما تبعت request لـ `localhost:5001/WeatherForecast` مثلاً، الـ API هترجعلك بيانات عن الطقس للأيام الجاية في شكل JSON زي ده:

```json
[
    {
        "date": "2024-10-16T10:22:32.843Z",
        "temperatureC": 25,
        "temperatureF": 77,
        "summary": "Mild"
    },
    {
        "date": "2024-10-17T10:22:32.843Z",
        "temperatureC": 10,
        "temperatureF": 50,
        "summary": "Bracing"
    }
]
```