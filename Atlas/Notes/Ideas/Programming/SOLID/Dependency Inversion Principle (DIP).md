---
up:
  - "[[SOLID Principles]]"
related: 
created: 2024-10-17
---


هو واحد من أهم المبادئ في **SOLID Principles**، وبيساعدك تفصل ما بين الأجزاء المختلفة في الكود بتاعك بشكل يخلي الصيانة أسهل والاختبار أذكى. 
أول حاجة هو معتمد على [[Cs Abstraction]]

## فكرة الـ Tight Coupling والـ Loose Coupling:
خليني أبدأ بمثال عملي عشان نفهم الفكرة. 

- **المفك العادي:** لما تجيب مفك (بيد ومسمار ثابتين) وتفصل الرأس بتاعته عن اليد، المفك كله بيبطل يشتغل، صح؟ ده مثال على **Tight Coupling** (اعتمادية شديدة)، بمعنى إن مافيش مرونة في استبدال أجزاء من النظام.
![[Pasted image 20241017002920.png]]
- **مفك برأس متغيرة:** في المقابل، المفك اللي ليه رأس ممكن تتغير هو مثال على **Loose Coupling**، لأنك تقدر تبدل الرأس براحتك بدون ما يبطل المفك يشتغل. ده اللي الـ DIP بيحاول يعمله في الكود بتاعك، وهو إنك تقلل الاعتمادية بين الأجزاء المختلفة من البرنامج.
![[Pasted image 20241017002945.png]]

---

## يعني إيه Dependency Inversion Principle؟
الـ **DIP** بيقول: 
1. الـ**High-level modules** (الكود اللي فيه منطق الأعمال - Business Logic) ما يعتمدش بشكل مباشر على **low-level modules** (زي الكود اللي بيتعامل مع قاعدة البيانات أو تسجيل الدخول). 
2. الاتنين لازم يعتمدوا على **Abstractions** (زي **Interfaces**).
3. الـ Abstractions المفروض متهتمش بالتفاصيل بس التفاصيل هي اللي تهتم بالـ Abstractions

**يعني إيه؟**  
يعني بدل ما كل كلاس ينادي على كلاس تاني بشكل مباشر (ويعمل `new` لكائن جديد)، نخليهم كلهم يعتمدوا على واجهة عامة **[[Cs Interface]]**. 
الهدف إن لو حبينا نغير في التفاصيل بعد كده، ما نحتاجش نعدل كل الكود اللي بيعتمد على التفاصيل دي.

---

## كود بدون DIP (Tight Coupling):
### **كود برنامج توظيف (Job Application Manager):**

#### **Program.cs:**
```csharp
var jobManager = new JobApplicationManager();
var applicant = new Applicant
{
    Name = "Ahmed",
    BirthDate = new DateTime(1990, 1, 1)
};
jobManager.SubmitApplication(applicant);
```

#### **JobApplicationManager.cs:**
```csharp
public class JobApplicationManager
{
    public void SubmitApplication(Applicant applicant)
    {
        var logger = new Logger();
        logger.Log("Submitting application");

        var emailSender = new EmailSender();
        emailSender.Send("Application submitted");
    }
}
```

- **المشكلة:**  
في المثال ده، كل مرة `JobApplicationManager` بيحتاج **Logger** أو **EmailSender**، بيعمل `new` لكل واحد فيهم. 
ده معناه إن فيه **Tight Coupling** بين الكلاسات، ولو حبينا نغير في طريقة تسجيل الأحداث أو إرسال الإيميلات، هنضطر نعدل كل مكان استخدم فيه الكائنات دي.
بالنسبة للـ Main class فالـ Job class دا عبارة عن Low level والـ Main نفسه هو الـ High level
بالنسبة للـ Job class فهو High-level والـ logger  class دا Low-level

---

## تطبيق DIP (Loose Coupling) باستخدام Interfaces وDI:
الـ Dependency Inversion دا المبدأ العام و الـ [[Dependency Injection]] دا إحدى الطرق اللي بتتطبق بيها المبدأ دا

### [[Cs Interface]]
#### حل المشكلة باستخدام Interfaces:
هنبدأ بإننا نعرّف **Interfaces** لكل من **Logger** و**EmailSender**.

##### **ILogger Interface:**
```csharp
public interface ILogger
{
    void Log(string message);
}
```

##### **EmailSender Interface:**
```csharp
public interface IEmailSender
{
    void Send(string message);
}
```


#### كود مُحسن باستخدام DIP:

##### **Logger.cs:**
```csharp
public class Logger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
}
```

##### **EmailSender.cs:**
```csharp
public class EmailSender : IEmailSender
{
    public void Send(string message)
    {
        Console.WriteLine($"Email sent: {message}");
    }
}
```

##### **JobApplicationManager.cs:**
```csharp
public class JobApplicationManager
{
    private readonly ILogger _logger;
    private readonly IEmailSender _emailSender;

    public JobApplicationManager(ILogger logger, IEmailSender emailSender)
    {
        _logger = logger;
        _emailSender = emailSender;
    }

    public void SubmitApplication(Applicant applicant)
    {
        _logger.Log("Submitting application");
        _emailSender.Send("Application submitted");
    }
}
```

---

#### الـProgram.cs بعد تطبيق DIP:
```csharp
var logger = new Logger();
var emailSender = new EmailSender();
var jobManager = new JobApplicationManager(logger, emailSender);

var applicant = new Applicant
{
    Name = "Ahmed",
    BirthDate = new DateTime(1990, 1, 1)
};

jobManager.SubmitApplication(applicant);
```

- **إيه الفرق هنا؟**  
دلوقتي، بدل ما `JobApplicationManager` هو اللي يعمل `new` بنفسه لكل من **Logger** و**EmailSender**، إحنا بنمررهم ليه من بره. 
وبكده قدرنا نحقق **Loose Coupling** بين الأجزاء المختلفة.

---

### **تطبيق DIP باستخدام Dependency Injection (DI):**
الخطوة الجاية إننا نستخدم **Dependency Injection** (DI)، وده هيكون عن طريق **ASP.NET Core DI Container**.

#### **تسجيل الخدمات في Program.cs:**
```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddScoped<ILogger, Logger>();
builder.Services.AddScoped<IEmailSender, EmailSender>();
builder.Services.AddScoped<JobApplicationManager>();

var app = builder.Build();
app.Run();
```


#### **استخدام JobApplicationManager في Controller:**
```csharp
[ApiController]
[Route("[controller]")]
public class JobApplicationController : ControllerBase
{
    private readonly JobApplicationManager _jobManager;

    public JobApplicationController(JobApplicationManager jobManager)
    {
        _jobManager = jobManager;
    }

    [HttpPost]
    public IActionResult Submit(Applicant applicant)
    {
        _jobManager.SubmitApplication(applicant);
        return Ok();
    }
}
```

---
## Factory 
هو اسخدم على JobApplicationManager class مبدأ الـ [[Factory]] عشان يظبطها
## **الخلاصة:**
- الـ**Dependency Inversion Principle (DIP)** بيقولك إن الكود اللي فيه منطق الأعمال ما يعتمدش بشكل مباشر على التفاصيل.  
- الطريقة الأسهل لتطبيق DIP هي استخدام **Dependency Injection (DI)**، اللي بيسمح لك تفصل ما بين الكلاسات وتحقن الكائنات اللي محتاجها كل كائن.  
- باستخدام DI، الكود بتاعك بيبقى أنظف وأسهل في الصيانة، وبتقدر تعمل **Unit Testing** بشكل أذكى.
