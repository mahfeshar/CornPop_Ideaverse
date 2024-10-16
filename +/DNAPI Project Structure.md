

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

كلمة `ApiController` دي بنقول عليها Attribute أو Decoration لأنها بتخلي الـ Function يغير الديكور بتاعه ويعمل حاجات مكنش بيعملها، واستعملنا واحدة زيها قبل كدا في الـ [[Cs Enums]]
## الفرق في الوراثة بين MVC و API:
- في الـ **MVC**:
  - الـ Controller بيورث من **Controller** class وهو بيبقا وارث من الـ `BaseController`.
  - بيورث من كلاس وارث ليه؟ 
    بيكون عنده حاجات إضافية زي **`ViewData`** و`TempData` اللي بتتعامل مع البيانات قبل ما توصل للمستخدم.

- في الـ **API**:
  - الـ Controller بيورث من **`BaseController`** على طول.
  - مش بيحتاج أي `ViewData` أو `TempData` لأنه مش بيرجع بيانات كـ View.
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

## مثال على استخدام الـ Dependency Injection مع الـ `DbContext`:
- هنا بنستخدم SQL Server كـ Database للـ API:
  ```csharp
  builder.Services.AddDbContext<StoreContext>(options => {
      options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"));
  });
  ```
  - الـ Dependency Injection هنا بتمكننا من استدعاء الـ DbContext بسهولة في أي مكان في الكود.

## ملف **`launchSettings.json`**:

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
  1. الـ**http**: تشغيل المشروع على **HTTP** باستخدام **Kestrel** على `http://localhost:5055`.
  2. الـ**https**: تشغيل المشروع على **HTTPS** و**HTTP** معًا على `https://localhost:7078` و `http://localhost:5055`.
  3. الـ**IIS Express**: بيشغل المشروع على IIS Express مع توثيق **Swagger**.

- كل البروفايلات بتستخدم بيئة **Development** وبتفتح الـ **Swagger** تلقائيًا بعد التشغيل.
## شرح `appsettings.json`:

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

## شرح **dummy example** بتاع الـ "WeatherForecast":

في بداية أي مشروع ASP.NET Core Web API، بيجي معاه **dummy example** بيبسط مفهوم الـ API عن طريق تقديم مثال بسيط اسمه **`WeatherForecast`**. 
ده عبارة عن كلاس بيستخدمه المشروع عشان يرجع بيانات وهمية (dummy data) عن درجات الحرارة المتوقعة، وده بيسهل فهم إزاي الـ API شغالة.

#### الكود
```csharp
public class WeatherForecast
{
    public DateTime Date { get; set; }  // تاريخ اليوم
    public int TemperatureC { get; set; }  // درجة الحرارة بالـ Celsius
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);  // حساب درجة الحرارة بالـ Fahrenheit
    public string? Summary { get; set; }  // وصف الطقس (مشمس، ممطر، إلخ)
}
```

#### الـController بتاع WeatherForecast:

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

##### النتيجة:
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