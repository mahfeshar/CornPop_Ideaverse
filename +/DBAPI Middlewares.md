
## يعني إيه Middleware؟  
تخيل إن عندك فيلا (الله يوسع علينا وعليك). عند مدخل الفيلا، فيه حارس أمن والبواب. أي حد يدخل، لازم يعدي الأول على الحارس يفتشه وبعد كده البواب يفتحله البوابة. 
لما يجي حد يخرج، نفس الموضوع، بس بالعكس: يعدي على البواب الأول وبعدين على حارس الأمن.  

نفس الكلام ده بالظبط بيحصل في التطبيق، كل **Request** بيدخل بيعدي على **Middlewares**، وكل **Response** بيخرج يعدي عليهم برضو. 
ممكن الميدل وير يسمح للطلب يدخل زي ما هو، أو يرفضه، أو حتى يعدل عليه، ونفس الكلام مع الرد وهو راجع. 

في الـ Program أي حاجة فيها `app.Use` هي عبارة عن Middleware ومن غيرها البرنامج مش هيشتغل
```cs
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

app.UseAuthorization();
```

---

## إزاي بيشتغل Middleware في ASP.NET Core؟  
الـ Middlewares بتكون على شكل **Pipeline**، يعني كل **Request** بيعدي على أكثر من Middleware واحد ورا التاني، ولما الطلب يوصل لآخر Middleware، يتم معالجته ويرجع الرد بنفس الترتيب العكسي.

![[Pasted image 20241018080329.png]]

---

## الكود الأساسي لعمل Middleware مخصص  
له كذا طريقة زي `app.Run`, `app.Map` ومش هنشرحهم هنا دلوقتي وعادة مش بيتم استخدامهم كتير.
بس هنطبق الطريقة التالتة وهي الأقوى وهي اللي هنشتغل بيها


### إنشاء كلاس Middleware:
هنعمل Middleware يحسبلي الزمن اللي بياخده الـ Request وفيه حاجات جاهزة كدا
```cs
public class ProfileMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<ProfileMiddleware> _logger;

    public ProfileMiddleware(RequestDelegate next, ILogger<ProfileMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        var stopwatch = Stopwatch.StartNew();
        await _next(context);
        stopwatch.Stop();

        _logger.LogInformation($"Request {context.Request.Path} took {stopwatch.ElapsedMilliseconds} ms");
    }
}
```

- الـ`RequestDelegate`: دي مهمة علشان نمرر الطلب للـ Middleware اللي بعده. (**أساسي**)
- الـ`ILogger`: بنستخدمه لتسجيل الوقت اللي أخده الطلب عشان ينفذ.
- الـ`InvokeAsync`: دي الميثود الأساسية في أي Middleware، اللي بتستقبل الـ **HttpContext** اللي بيشيل كل المعلومات عن الطلب والرد. (**أساسي**)

---

## تسجيل الـ Middleware في التطبيق  
لازم نضيف الـ Middleware في الـ **Program.cs** عشان يتم تنفيذه ضمن الـ Pipeline.

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddSwaggerGen();

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseMiddleware<ProfileMiddleware>();

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
app.Run();
```

### تشغيل الـ Middleware
دلوقتي لما تبعت أي **Request** من خلال Swagger، هتشوف اللوج بيتسجل في نافذة الـ Output مع وقت التنفيذ.

---

### إنشاء Middleware جديد لتحديد عدد الطلبات (Rate Limiting)  

#### **RateLimitingMiddleware.cs**:
```csharp
public class RateLimitingMiddleware
{
    private static int _requestCount = 0;
    private static DateTime _lastRequestTime = DateTime.MinValue;
    private readonly RequestDelegate _next;

    public RateLimitingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        if ((DateTime.Now - _lastRequestTime).TotalSeconds > 10)
        {
            _requestCount = 1;
            _lastRequestTime = DateTime.Now;
        }
        else if (_requestCount >= 5)
        {
            context.Response.StatusCode = 429; // Too Many Requests
            await context.Response.WriteAsync("Rate limit exceeded. Please try again later.");
            return;
        }
        else
        {
            _requestCount++;
        }

        await _next(context);
    }
}
```

### شرح الكود:
- **`_requestCount`**: عدد الطلبات اللي بعتها المستخدم خلال 10 ثواني.
- **`_lastRequestTime`**: آخر وقت تم فيه إرسال طلب.
- **Status Code 429**: بيتم إرجاعه لو المستخدم تجاوز الحد المسموح للطلبات.

---

### تسجيل Middleware التحكم في عدد الطلبات:
```csharp
app.UseMiddleware<RateLimitingMiddleware>();
```

---

### تجربة الـ Middlewares باستخدام Swagger  
1. شغل التطبيق وافتح Swagger:  
   `https://localhost:5001/swagger/index.html`

2. جرب تبعت أكتر من 5 طلبات خلال 10 ثواني، هتلاقي التطبيق بيرجع:  
   **429 Too Many Requests** مع رسالة "Rate limit exceeded."

---

### الخاتمة  
الـ Middlewares جزء أساسي في أي تطبيق **ASP.NET Core**. شفنا إزاي نعمل Middleware مخصص، وازاي نتحكم في عدد الطلبات باستخدام **Rate Limiting Middleware**.  

يا رب يكون الشرح واضح وبسيط ليكم، ولا تنسوا الدعاء لإخواننا في فلسطين، والسلام عليكم ورحمة الله وبركاته.