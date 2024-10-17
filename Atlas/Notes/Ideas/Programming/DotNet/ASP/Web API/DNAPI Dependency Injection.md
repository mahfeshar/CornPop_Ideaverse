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
في البرمجة، **dependency** هي أي حاجة (زي **class** أو **interface**) بيعتمد على Class أو Interface تاني.
فمثلاً، الكيبورد اللي بكتب بيه هو dependency بالنسبة لي، والماوس اللي بحركه برضه dependency. 

يعني باختصار: **أي حاجة التطبيق بيعتمد عليها عشان يشتغل** هي dependency.

---

## إيه هو بقى Injection؟
كلمة **Injection** معناها "حقن"، يعني إحنا مش بنخلي الكائن (class) هو اللي ينشئ الـ dependency بنفسه، بل بنعمل **حقن للكائنات اللي بيعتمد عليها** من خارج الكود.  

> وده يخلي الكود بتاعك **أكتر مرونة وقابلية للاختبار**. بدل ما كل كائن يقرر بنفسه يعمل object جديد من اللي هو محتاجه، الكود هيطلب الـdependency من مكان خارجي، وهو اللي يبعته ليه.

---

### Program.cs
في المشاريع اللي بنبنيها بـASP.NET Core، الملف الأساسي اللي بيبدأ منه كل حاجة هو **`Program.cs`**. 
دلوقتي مع **top-level statements**، مش محتاج تكتب `namespace` ولا `class`، بل الكود بيتكتب مباشرة كأنه **سكريبت**.

ده مثال للكود اللي هيكون في **`Program.cs`**:

```csharp
var builder = WebApplication.CreateBuilder(args);

// إضافة الخدمات للـ Dependency Injection Container
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// تمكين Swagger في بيئة التطوير
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
app.Run();
```

---

### **إزاي الـDependency Injection بيشتغل؟**
- في المثال اللي فوق، لما بنكتب `builder.Services.AddControllers()`، إحنا بنقول للـ **DI Container** الخاص بـ ASP.NET Core إن في كائنات **Controllers** هنحتاجها في التطبيق.

- الـ**Swagger** كمان بيتم تسجيله عشان يشتغل في بيئة التطوير. واللي بيعمله ASP.NET إنه بيراقب الـ dependencies اللي انت سجلتها، ولما الكنترولر يحتاج حاجة، **الـContainer** بيبعتهاله تلقائيًا.

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

---

### **إزاي أسجل كائن في الـDI Container؟**
خلينا نفترض إن إحنا عايزين نفصل اللوجيك الخاص بالـ **WeatherForecast** في **Service** لوحدها. هنعمل **class** جديدة اسمها `WeatherForecastService`.

#### **WeatherForecastService:**
```csharp
public class *WeatherForecastService*
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

#### **تسجيل الـ Service في Program.cs:**
```csharp
builder.Services.AddScoped<WeatherForecastService>();
```

دلوقتي الـ **WeatherForecastService** بقت متاحة لأي كائن يحتاجها، والـ DI Container هيتكفل بإنشاء **instance** منها عند الطلب.

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

### **الخلاصة:**
الـ**Dependency Injection** هو أسلوب بيخليك تفصل الـ dependencies عن بعض، وتخلي **ASP.NET Core** هو المسؤول عن إنشاء وإدارة الكائنات اللي التطبيق محتاجها. 
ده بيخلي الكود أنظف وأسهل في الصيانة، وكمان بيسهل جدًا اختبار التطبيق. 
استخدام **Interfaces** بيديك مرونة أعلى، وبيفتح لك المجال إنك تغير الـ implementations بسهولة بدون ما تأثر على باقي الكود.