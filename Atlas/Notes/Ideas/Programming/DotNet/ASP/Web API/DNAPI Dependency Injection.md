---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-10-17
---

هنتكلم عن **Dependency Injection** (أو اختصارًا DI)، وعايزك تركز معايا كويس جدًا لإنه واحد من الركائز الأساسية في **ASP.NET Core**، ومستخدم بشكل كبير جدًا جدًا في معظم التطبيقات. 
الفكرة في DI مش معقدة، هي حاجة بسيطة جدًا.

لكن قبل ما نبدأ، لازم تكون فاهم [[SOLID Principles]] كويس، وبالأخص [[Dependency Inversion Principle (DIP)]] ، لأنه مرتبط جدًا بموضوعنا النهارده. 

---
## يعني إيه Dependency؟
الإعتمادية: إني أبقا معتمد على حاجة
ببساطة، **Dependency** معناها حاجة بتعتمد عليها. لو عندك **Class** أو **Method** في الكود بتعتمد على حاجة تانية، دي اسمها **Dependency**. 
يعني باختصار: **أي حاجة التطبيق بيعتمد عليها عشان يشتغل** هي dependency.
فمثلاً، الكيبورد اللي بكتب بيه هو dependency بالنسبة لي، والماوس اللي بحركه برضه dependency. 

أما **Injection**، فمعناها إننا بنحقن (نوفر) الـ Dependency اللي محتاجها الكود بدل ما ننشئها بنفسنا في كل مرة.

الفكرة الأساسية هنا إنك بدل ما تستخدم `new` كل مرة، بتطلب الـ Dependency دي في **Constructor**، و **ASP.NET Core** هي اللي بتوفرها بشكل تلقائي.

---
### **مثال عملي: Inject Logger في Controller**
تعالى نبص على كنترولر بسيط بيستخدم **ILogger** عشان يسجل الأحداث:

#### **WeatherForecastController:**
```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    private readonly ILogger<WeatherForecastController> _logger;

    //HERE
    public WeatherForecastController(ILogger<WeatherForecastController> logger)
    {
        _logger = logger;
    }

    [HttpGet]
    public IEnumerable<WeatherForecast> Get()
    {
        _logger.LogInformation("Getting weather data");
        return Enumerable.Range(1, 5).Select(index => new WeatherForecast
        {
            Date = DateTime.Now.AddDays(index),
            TemperatureC = Random.Shared.Next(-20, 55),
            Summary = "Cool"
        })
        .ToArray();
    }
}
```

- هنا بنشوف إزاي الـ **ILogger** بيتحقن في الكنترولر عن طريق الـ **constructor**. الكنترولر ده بيعتمد على **ILogger**، والـ **DI Container** هو اللي بيقوم بإنشاء **instance** من `ILogger` وبيديه للكنترولر.
- الـ**Constructor Injection**: هنا بنستخدم **ILogger** في الـ **Constructor** بدل ما ننشئه يدويًا.
- الـ**Log Information**: نكتب Log في كل مرة يتم فيها استدعاء الـ API، عشان نعرف وقت التشغيل لو حصلت أي مشكلة.

---

### بناء خدمة (Service) جديدة
دلوقتي هننقل المنطق اللي في `WeatherForecastController` لكلاس تاني، ونسميه **WeatherForecastService**، وده بيوضح إزاي الـ Dependency Injection بتشتغل مع الخدمات (Services).
```csharp
public interface IWeatherForecastService
{
    IEnumerable<WeatherForecast> GetForecast();
}

public class WeatherForecastService : IWeatherForecastService
{
    private readonly ILogger<WeatherForecastService> _logger;

    public WeatherForecastService(ILogger<WeatherForecastService> logger)
    {
        _logger = logger;
    }

    public IEnumerable<WeatherForecast> GetForecast()
    {
        _logger.LogInformation("Fetching weather forecast data");
        return Enumerable.Range(1, 5).Select(index => new WeatherForecast
        {
            Date = DateTime.Now.AddDays(index),
            TemperatureC = Random.Shared.Next(-20, 55),
            Summary = "Sample Data"
        }).ToArray();
    }
}

```

#### تحديث `Program.cs` لتسجيل الـ Service
```csharp
builder.Services.AddScoped<WeatherForecastService>();
```

عشان نستخدم الـ **Service** دي في المشروع، لازم نضيفها في الـ **DI Container** باستخدام `AddScoped`

---

### الـ**Lifetime في الـ DI:**
الـ Dependency هتفضل متاحة لحد امتا
- الـ**Transient:** يتم إنشاء **instance** جديد لكل طلب (كل مكان في البرنامج بعمله واحد له لوحده).
- الـ**Scoped:** يتم إنشاء **instance** جديد لكل طلب HTTP (للطلب كله). دا الـ *Default*
- الـ**Singleton:** يتم إنشاء **instance** واحدة فقط طول فترة حياة التطبيق (طول ما البرنامج شغال).

#### **مثال على تسجيل lifetimes:**
```csharp
builder.Services.AddTransient<MyService>(); // Transient
builder.Services.AddScoped<MyService>();    // Scoped
builder.Services.AddSingleton<MyService>(); // Singleton
```
آخر مرة هو اللي بيبقا له مفعول

---

### **ليه نستخدم Interfaces مع DI؟**
من الأفضل إننا نسجل **interfaces** بدل **classes** مباشرة. ليه؟  
- ده بيديك مرونة إنك تغير **implementation** في المستقبل بسهولة.
- بيسهل عملية **Unit Testing**، لأنك ممكن تستبدل الـ implementation بـ **mock object** أثناء الاختبار.

#### **مثال: Interface + Implementation:**
```csharp
public interface IWeatherService
{
    IEnumerable<WeatherForecast> GetForecast();
}

public class WeatherService : IWeatherService
{
    public IEnumerable<WeatherForecast> GetForecast()
    {
        return Enumerable.Range(1, 5).Select(index => new WeatherForecast
        {
            Date = DateTime.Now.AddDays(index),
            TemperatureC = Random.Shared.Next(-20, 55),
            Summary = "Cool"
        })
        .ToArray();
    }
}
```

#### **تسجيل Interface مع Implementation:**
```csharp
builder.Services.AddScoped<IWeatherService, WeatherService>();
```

---
### أهمية استخدام Dependency Injection

- **تنظيم الكود**: الكود بيبقى أنضف وأسهل في الإدارة.
- **المرونة**: ممكن تغير الـ Implementation بسهولة عن طريق تسجيل Services جديدة.
- **الوحدة (Unit Testing)**: بتساعدك في كتابة اختبارات أفضل لأنك بتقدر تستبدل الـ Services الحقيقية بـ **Mocks** أثناء الاختبار.
### **الخلاصة:**
الـ**Dependency Injection** هو أسلوب بيخليك تفصل الـ dependencies عن بعض، وتخلي **ASP.NET Core** هو المسؤول عن إنشاء وإدارة الكائنات اللي التطبيق محتاجها. 
ده بيخلي الكود أنظف وأسهل في الصيانة، وكمان بيسهل جدًا اختبار التطبيق. 
استخدام **Interfaces** بيديك مرونة أعلى، وبيفتح لك المجال إنك تغير الـ implementations بسهولة بدون ما تأثر على باقي الكود.