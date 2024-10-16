

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

### مثال على مشروع API:

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var builder = WebApplication.CreateBuilder(args);

        // Configure Services
        builder.Services.AddControllers();  // إضافة الـ Controllers مع الـ Dependency Injection

        // Swagger/OpenAPI
        builder.Services.AddEndpointsApiExplorer();
        builder.Services.AddSwaggerGen();  // لإضافة توثيق Swagger

        var app = builder.Build();

        // Middleware Configuration
        if (app.Environment.IsDevelopment())
        {
            app.UseSwagger();
            app.UseSwaggerUI();
        }

        app.UseHttpsRedirection();
        app.UseAuthorization();

        app.MapControllers();  // لتحديد الـ routes الخاصة بالـ Controllers
        app.Run();  // لتشغيل التطبيق
    }
}
```

## استخدام Postman واختبار الـ API:
- بعد تشغيل المشروع، بتفتح **Postman** وتضيف الـ URL الخاص بالـ API (اللي بيكون عادةً **localhost**).
- بتعمل Request لكل Endpoint عشان تجرب الـ API.
- تقدر تعمل **Export** للـ Collection من Postman عشان تبعته لأي حد يشتغل معاك على المشروع.

#### RESTful APIs:
- الـ REST API بتشتغل على أساس الـ HTTP Verbs زي **GET**، **POST**، **PUT**، و**DELETE**.
- مثلاً، لو بعت **GET** request، الـ API هيرد بالبيانات، ولو بعت **POST** هيضيف البيانات.

#### مميزات .NET 6 و .NET 8:
- في .NET 6 تم دمج ملفات الـ `Program` و `Startup` في ملف واحد لتبسيط الكود.
- في .NET 8، التحسينات بتركز أكتر على الأداء وزيادة دعم مميزات زي الـ **Blazor** والـ **Minimal APIs**، بالإضافة إلى تحسينات كبيرة في سرعة الاستجابة وتطوير الأدوات الخاصة بالـ Developer Experience.

#### مثال على استخدام الـ Dependency Injection مع الـ DbContext:
- هنا بنستخدم SQL Server كـ Database للـ API:
  ```csharp
  builder.Services.AddDbContext<StoreContext>(options => {
      options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"));
  });
  ```
  - الـ Dependency Injection هنا بتمكننا من استدعاء الـ DbContext بسهولة في أي مكان في الكود.

---

### ملف **launchSettings.json**:
الـ **launchSettings.json** بيحدد إعدادات التشغيل الخاصة بالمشروع في وضع التطوير (Development). وده بيشمل الـ profiles اللي بتحدد إزاي المشروع هيشتغل.

##### مثال على ملف **launchSettings.json**:
```json
{
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "Kestrel": {
      "commandName": "Project",
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001;http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "WebApi": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001;http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

#### شرح محتويات الملف:
- **profiles**: بيحدد الـ profiles المختلفة اللي بتشغل المشروع.
  - **IIS Express**: ده بيستخدم الـ IIS Express لتشغيل المشروع.
  - **Kestrel**: بيستخدم الـ Kestrel server لتشغيل المشروع مباشرة على الـ localhost.
  - **WebApi**: بيشغل المشروع كـ Console Application باستخدام الـ URLs المحددة.

- **ASPNETCORE_ENVIRONMENT**: بيحدد بيئة التشغيل (هنا هي "Development").
- **launchBrowser**: لو true، هيفتح المتصفح تلقائيًا على الـ URL بتاع المشروع بعد تشغيله.

---

ده كان الشرح النهائي للسيشن الأولى بالتفصيل المطلوب ومع التعديلات والإضافات اللي طلبتها. لو عندك أي استفسار إضافي أو محتاج شرح أكتر في أي جزء، أنا موجود!