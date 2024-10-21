---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-10-21
---
معتمد على الـ [[DBAPI Middlewares]]

![[Pasted image 20241021051718.png]]
### يعني إيه Action Filters؟
الـ **Action Filters** عبارة عن **فلتر** بيراقب الـ **Action Methods** اللي جوه الكنترولر. 
أي **Method** بتعرضها كـ API سواء كانت `GetProductById` أو `CreateProduct` أو `DeleteProduct`، ممكن تضيف عليها فلتر بحيث:
- **يعدل** في الداتا وهي داخلة.
- **يعدل** في الرد قبل ما يخرج.
- أو **يمنع** العملية لو في حاجة مش مظبوطة.

ببساطة، هو زي **حارس أمن** واقف على الـ **Action**، بيفتش البيانات الداخلة، ولو الأمور تمام يسمح لها تدخل. 
نفس الكلام بيحصل مع الرد وهو راجع، ممكن الفلتر يعدل فيه أو يمنعه من الخروج.

---

### الفرق بين Middlewares وAction Filters  
تخيل إن الفيلا بتاعتك ليها **بوابتين**:
1. **البوابة الخارجية**: دي هي الـ **[[DBAPI Middlewares]]**، أي **Request** بيوصل لازم يعدي من خلالها الأول.
2. **البوابة الداخلية**: دي هي الـ **Action Filters**، بتشتغل جوه الكنترولر وعلى مستوى الـ **Methods**.

فيه اختلافات أساسية بين الاثنين:
- الـ **Middleware** بيشتغل على كل **Request** جاي للسيرفر، حتى لو كان طلب لصورة أو ملف PDF.
- الـ **Action Filters** بيشتغلوا بس على **Actions**، يعني لما يوصل الطلب لكنترولر معين.

---

### الكود الأساسي لإنشاء Action Filter  

#### إنشاء فلتر بسيط  
```csharp
public class LogActivityFilter : IActionFilter
{
    private readonly ILogger<LogActivityFilter> _logger;

    public LogActivityFilter(ILogger<LogActivityFilter> logger)
    {
        _logger = logger;
    }

    public void OnActionExecuting(ActionExecutingContext context)
    {
        _logger.LogInformation($"Executing {context.ActionDescriptor.DisplayName}");
    }

    public void OnActionExecuted(ActionExecutedContext context)
    {
        _logger.LogInformation($"Executed {context.ActionDescriptor.DisplayName}");
    }
}
```

#### شرح الكود:  
- الـ`IActionFilter`: ده الـ **Interface** اللي بنبني منه الفلتر. لازم نطبق **OnActionExecuting** و**OnActionExecuted**.
- الـ`OnActionExecuting`: دي بتشتغل قبل تنفيذ الـ **Action**.
- الـ`OnActionExecuted`: دي بتشتغل بعد ما الـ **Action** ينفذ وتقدر تعدل في الرد.

---


#### تسجيل كـ Global Filter  
لو عايز تطبق الفلتر على كل **Actions** في التطبيق، سجل الفلتر بالشكل ده في **Program.cs**:
دي طريقة التسجيل ك Global هيشتغل على أي Action عندي بتحصل
```csharp
builder.Services.AddControllers(options =>
{
    options.Filters.Add<LogActivityFilter>();
	options.Filters.Add<LogActivityFilter>();
	// More Filters
);
```
لما تبدأ تشغله بيبدأ يروح الأول لـ `OnActionExecuting` وبعدين يعمل Action وبعدين `OnActionExecuted`

#### تطبيق الفلتر على كنترولر معين  
ممكن تطبقه على كنترولر معين بس، عن طريق إضافة الفلتر فوق الكنترولر بالشكل ده:

```csharp
[ServiceFilter(typeof(LogActivityFilter))]
public class ProductController : ControllerBase
{
    // Actions هنا
}
```

#### تطبيق الفلتر على Method معين  
ولو عايز تطبقه على **Method** واحدة بس، حط الفلتر فوقها كده:

```csharp
[ServiceFilter(typeof(LogActivityFilter))]
public IActionResult GetProductById(int id)
{
    // كود الميثود
}
```

---

### تجربة الفلتر باستخدام Swagger  
بعد ما تسجل الفلتر وتعمل Run للتطبيق، افتح **Swagger** على الرابط التالي:  
`https://localhost:5001/swagger/index.html`

1. جرب تنفذ أي **Request** وشوف الـ Logs في نافذة الـ Output.
2. هتلاقي كل **Request** بيتم تسجيله قبل وبعد تنفيذه.

---

### شرح الـ Result, Arguments
### مثال إضافي على Action Filter باستخدام Async  

```csharp
public class AsyncLogActivityFilter : IAsyncActionFilter
{
    private readonly ILogger<AsyncLogActivityFilter> _logger;

    public AsyncLogActivityFilter(ILogger<AsyncLogActivityFilter> logger)
    {
        _logger = logger;
    }

    public async Task OnActionExecutionAsync(ActionExecutingContext context, ActionExecutionDelegate next)
    {
        _logger.LogInformation($"Executing {context.ActionDescriptor.DisplayName}");
        await next();  // نفذ الـ Action
        _logger.LogInformation($"Executed {context.ActionDescriptor.DisplayName}");
    }
}
```

#### شرح الكود:  
- **`IAsyncActionFilter`**: ده فلتر **Async** لو عايز الفلتر يشتغل بشكل غير متزامن.
- **`ActionExecutionDelegate next`**: ده بيمرر الطلب للـ **Action** اللي بعده.

---

### الفرق بين الفلتر المتزامن والغير متزامن  
- **IActionFilter**: بيشتغل بشكل عادي ومتزامن.
- **IAsyncActionFilter**: بيشتغل بشكل غير متزامن باستخدام **async/await**. 

---

### خلاصة الفرق بين Action Filters وMiddlewares  
1. **السكوب**:  
   - الـ **Middleware** بيشتغل على مستوى التطبيق بالكامل.  
   - الـ **Action Filters** تقدر تحددها على مستوى كنترولر أو Method معينة.

2. **التحكم في البيانات**:  
   - الـ **Middleware** مش بيعرف معلومات عن الكنترولر أو الـ Action، بيشتغل على مستوى الـ URL.  
   - الـ **Action Filters** بيعرف تفاصيل عن الـ Method والـ Parameters.

3. **الهدف**:  
   - الـ **Middleware** بيشتغل على أي طلب جاي، حتى لو كان طلب لملف.  
   - الـ **Action Filters** بيشتغل بس على الطلبات اللي بتتعامل مع كنترولرز وActions.

---

### الخاتمة  
الـ **Action Filters** من الأدوات المهمة جدًا في **ASP.NET Core** وبتساعدك تتحكم في الطلبات بشكل دقيق. تقدر تطبقها على مستوى التطبيق، الكنترولر، أو الـ Method. أتمنى تكون الفكرة وضحت، ولو حسيت إن الموضوع طويل شوية أو متعب، معلش، الشرح ده مهم جدًا علشان تستوعب الفرق بين **Middlewares** و**Action Filters** وتستخدمهم بشكل صح.

نشوفكم في الفيديو الجاي إن شاء الله. ولا تنسوا الدعاء لإخوانكم في فلسطين. السلام عليكم ورحمة الله وبركاته.