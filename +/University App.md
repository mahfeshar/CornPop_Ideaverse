# Code from Abdelmohsen
[university\_script](https://www.mediafire.com/file/lf6b7s0sud60erf/university_script.rar/file)

```cs
cmd = new SqlCommand("Portal_Get_SSO_DATA", con);
cmd.CommandType = CommandType.StoredProcedure;

SqlParameter p1 = new SqlParameter("@national_number", Session["national_number"].ToString());
SqlParameter p2 = new SqlParameter("@LoginType", Session["LoginType"].ToString());
```

في هذا الكود، يتم إعداد استعلام لاسترجاع البيانات من قاعدة بيانات SQL Server باستخدام الإجراء المخزن المسمى `"Portal_Get_SSO_DATA"`. 

هنا شرح كل خطوة:

1. **إنشاء كائن `SqlCommand`:**
   ```csharp
   cmd = new SqlCommand("Portal_Get_SSO_DATA", con);
   ```
   يتم هنا إنشاء كائن `SqlCommand` يسمى `cmd` ويستخدم اسم الإجراء المخزن `"Portal_Get_SSO_DATA"` والمتصل بقاعدة البيانات `con`.

2. **تحديد نوع الاستعلام كإجراء مخزن:**
   ```csharp
   cmd.CommandType = CommandType.StoredProcedure;
   ```
   هذه السطر يحدد أن `cmd` هو إجراء مخزن (`Stored Procedure`) في قاعدة البيانات.

3. **إضافة المعلمات (Parameters):**
   - **`@national_number`**:
     ```csharp
     SqlParameter p1 = new SqlParameter("@national_number", Session["national_number"].ToString());
     ```
     يتم إنشاء معلمة `SqlParameter` تسمى `p1` لتمرير قيمة رقم الهوية (`national_number`) للإجراء المخزن. هذه القيمة مسترجعة من جلسة المستخدم (`Session`) وتحول إلى نص باستخدام `ToString()`.

   - **`@LoginType`**:
     ```csharp
     SqlParameter p2 = new SqlParameter("@LoginType", Session["LoginType"].ToString());
     ```
     يتم إنشاء معلمة `SqlParameter` تسمى `p2` لتمرير نوع تسجيل الدخول (`LoginType`).
# Database
شغلنا الداتا بيز وأول حاجة شوفتها انه عملها في فايلات معروفة لوكال وانا غيرتها لفايلات عندي عالجهاز

فيه داتا كتير ومعلومات معرفهاش

عمل Alter لمعلومات كتير في السيتنجز بتاعها

عمل اتنين يوزر جديد
شوفت اليوزرز بتاعي عالويندوز 
CREATE USER [اسم_الجهاز\اسم_المستخدم] WITH DEFAULT_SCHEMA=[dbo]
Win + R -> lusrmgr.msc (CMD: net user - PS: Get-LocalUser)
PC name (My-PC -> Properites)

----

SET ANSI_NULLS
SET QUOTED_IDENTIFIER

دي عشان تشوف اليوزر نيم الموجود
USE YourDatabaseName;
GO
SELECT name 
FROM sys.database_principals 
WHERE sid = SUSER_SID('CornPop\mahfeshar');



# Using Stored Procedure
لإنشاء **API** يعتمد على **Stored Procedure** يقوم بالتحقق من بيانات تسجيل الدخول باستخدام `@national_number` و `@LoginType`، سنقوم بإنشاء **API** بسيط باستخدام **ASP.NET Core** مع شرح الكود بالتفصيل.

### الخطوات الرئيسية:
1. إعداد API Controller للـ Login.
2. إعداد `SqlCommand` للتعامل مع **Stored Procedure**.
3. التعامل مع **parameters** (`@national_number` و `@LoginType`) لتمريرها إلى الـ **Stored Procedure**.
4. الحصول على النتيجة من **Stored Procedure** للتحقق من صحة بيانات المستخدم.

### الكود النهائي وتفصيل الخطوات

#### الخطوة 1: إنشاء `LoginController`

في مشروع **ASP.NET Core**، قم بإنشاء **API Controller** جديد يُسمى `LoginController` لتتمكن من استقبال طلبات تسجيل الدخول.

```csharp
using Microsoft.AspNetCore.Mvc;
using System.Data;
using System.Data.SqlClient;
using System.Threading.Tasks;

namespace UniversityApp.API.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class LoginController : ControllerBase
    {
        private readonly string _connectionString;

        public LoginController(IConfiguration configuration)
        {
            // قراءة سلسلة الاتصال من ملف appsettings.json
            _connectionString = configuration.GetConnectionString("DefaultConnection");
        }

        [HttpPost]
        public async Task<IActionResult> Login([FromBody] LoginRequest loginRequest)
        {
            // تحقق من أن البيانات المدخلة ليست فارغة
            if (string.IsNullOrEmpty(loginRequest.NationalNumber) || string.IsNullOrEmpty(loginRequest.LoginType))
            {
                return BadRequest("National Number and Login Type are required.");
            }

            try
            {
                using (SqlConnection con = new SqlConnection(_connectionString))
                {
                    using (SqlCommand cmd = new SqlCommand("Portal_Get_SSO_DATA", con))
                    {
                        cmd.CommandType = CommandType.StoredProcedure;

                        // إعداد الـ parameters وإضافة القيم من الطلب
                        cmd.Parameters.Add(new SqlParameter("@national_number", loginRequest.NationalNumber));
                        cmd.Parameters.Add(new SqlParameter("@LoginType", loginRequest.LoginType));

                        // فتح الاتصال بقاعدة البيانات
                        await con.OpenAsync();

                        // تنفيذ الـ Stored Procedure
                        using (SqlDataReader reader = await cmd.ExecuteReaderAsync())
                        {
                            if (reader.HasRows)
                            {
                                // قراءة البيانات المتاحة من الـ Stored Procedure
                                while (await reader.ReadAsync())
                                {
                                    // لنقل أن الـ Stored Procedure ترجع معلومات المستخدم
                                    var userData = new
                                    {
                                        UserId = reader["UserId"],
                                        UserName = reader["UserName"],
                                        Role = reader["Role"]
                                    };

                                    // إرجاع البيانات كموافقة تسجيل دخول ناجحة
                                    return Ok(userData);
                                }
                            }
                            else
                            {
                                return Unauthorized("Invalid credentials.");
                            }
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                return StatusCode(500, $"Internal server error: {ex.Message}");
            }

            return Unauthorized("Invalid credentials.");
        }
    }
}
```

### شرح الكود بالتفصيل

#### 1. إعداد `LoginController`
- نبدأ بتعريف `LoginController` وتعيين مسار الوصول له (`[Route("api/[controller]")`)، بحيث يمكن الوصول إليه عبر `api/Login`.
- في الـ `constructor`، نقوم بقراءة سلسلة الاتصال من `appsettings.json` وتخزينها في متغير `_connectionString`.

#### 2. تعريف `Login` Endpoint
- قمنا بتعريف دالة `Login` التي تستقبل `HttpPost` وتقبل كائن `LoginRequest` يحتوي على `NationalNumber` و `LoginType`.

#### 3. التحقق من المدخلات
- قبل الاتصال بقاعدة البيانات، نقوم بالتحقق من أن `NationalNumber` و `LoginType` ليست فارغة. إذا كانت فارغة، نعيد `BadRequest`.

#### 4. إعداد الاتصال بـ SQL Server والـ Stored Procedure
- نستخدم `SqlConnection` للاتصال بقاعدة البيانات باستخدام `_connectionString`.
- نعرّف `SqlCommand` ونحدد اسم الـ **Stored Procedure** (`Portal_Get_SSO_DATA`).
- نحدد نوع الأمر كـ `CommandType.StoredProcedure`، وهذا يخبر `SqlCommand` أنه يجب تشغيل **Stored Procedure**.

#### 5. إضافة `Parameters` للـ Stored Procedure
- نضيف القيم من `loginRequest` (التي تأتي من طلب المستخدم) إلى **Stored Procedure** كـ parameters.
  ```csharp
  cmd.Parameters.Add(new SqlParameter("@national_number", loginRequest.NationalNumber));
  cmd.Parameters.Add(new SqlParameter("@LoginType", loginRequest.LoginType));
  ```

#### 6. تنفيذ Stored Procedure والحصول على النتائج
- نفتح الاتصال بقاعدة البيانات باستخدام `await con.OpenAsync()`.
- ننفذ الـ **Stored Procedure** وننتظر النتيجة باستخدام `ExecuteReaderAsync()`، ثم نتحقق من وجود صفوف (`reader.HasRows`).
- إذا تم العثور على بيانات، نقوم بقراءة البيانات من `SqlDataReader` وتكوين كائن `userData` يحتوي على بيانات المستخدم.
- إذا لم يتم العثور على أي صف، نعيد `Unauthorized` للدلالة على فشل تسجيل الدخول.

#### 7. التعامل مع الأخطاء
- إذا حدث خطأ أثناء الاتصال بقاعدة البيانات أو أثناء تنفيذ العملية، نقوم بإرجاع خطأ داخلي (`StatusCode 500`) يحتوي على رسالة الخطأ.

### كائن طلب تسجيل الدخول `LoginRequest`
للتأكد من أننا نستقبل البيانات في شكل مناسب، نستخدم كائن `LoginRequest` لتغليف المدخلات:

```csharp
public class LoginRequest
{
    public string NationalNumber { get; set; }
    public string LoginType { get; set; }
}
```

### إعداد `appsettings.json` لسلسلة الاتصال
تأكد من أن لديك سلسلة الاتصال مضبوطة في `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=your_server;Database=your_database;User Id=your_user;Password=your_password;"
  }
}
```

### النتيجة
- عند إرسال طلب **POST** إلى `api/Login` باستخدام `NationalNumber` و `LoginType`، يقوم الـAPI بتشغيل **Stored Procedure** وتحقق من صحة البيانات.
- إذا كانت البيانات صحيحة، يعيد الـAPI بيانات المستخدم.
- إذا كانت البيانات غير صحيحة، يعيد `Unauthorized`.

هذا هو كل شيء بالتفصيل عن كيفية إعداد **API** للتعامل مع **Stored Procedure** والتحقق من بيانات تسجيل الدخول.

# File Structure 
لتنظيم المشروع بشكل جيد على GitHub واستخدام Onion Architecture في .NET لمشروعك، يمكنك اتباع الهيكلية التالية التي تناسب هذا النوع من المشاريع.

### هيكلية المشروع على GitHub
على GitHub، يمكنك تنظيم الملفات والمجلدات كالتالي:

```
MyApp/
│
├── .github/                 # ملفات CI/CD أو GitHub Actions إن وجدت
│
├── docs/                    # وثائق المشروع مثل دليل الاستخدام والـREADME
│
├── src/                     # المجلد الرئيسي لمصدر الكود
│   ├── MyApp.Backend/       # مشروع الـ .NET للباك إند
│   └── MyApp.Frontend/      # مشروع Flutter للفرونت إند
│
├── tests/                   # الاختبارات الخاصة بالمشروع
│   ├── MyApp.Backend.Tests/ # اختبارات الباك إند
│   └── MyApp.Frontend.Tests/ # اختبارات الفرونت إند
│
├── README.md                # نظرة عامة على المشروع وكيفية تشغيله
├── .gitignore               # لتجاهل الملفات الغير مهمة
└── LICENSE                  # الرخصة الخاصة بالمشروع
```

### هيكلية الباك إند في فيجوال ستوديو باستخدام Onion Architecture

عند تنظيم مشروعك داخل Visual Studio بناءً على Onion Architecture، يمكنك تقسيم الطبقات في Solution كالتالي:

```
MyApp.Backend/
│
├── Core/                    # المجلد الذي يحتوي على الطبقات الأساسية للمشروع
│   ├── MyApp.Domain/        # تحتوي على الكيانات (Entities) والقواعد الأساسية للأعمال
│   └── MyApp.Application/   # تحتوي على الخدمات وواجهات التطبيقات
│
├── Infrastructure/          # المجلد الذي يحتوي على تطبيق قواعد البيانات وغيرها
│   ├── MyApp.Persistence/   # مسؤول عن إدارة الوصول للبيانات
│   └── MyApp.Infrastructure/ # أي خدمات خارجية أخرى
│
├── WebApi/                  # الواجهة البرمجية للتطبيق (API)
│   └── MyApp.WebApi/        # يحتوي على Controllers والنقاط النهائية (Endpoints)
│
└── Tests/                   # الاختبارات الخاصة بالباك إند
    ├── MyApp.Domain.Tests/  # اختبارات النطاق
    └── MyApp.Application.Tests/ # اختبارات الطبقة التطبيقية
```

### توضيحات إضافية

- **MyApp.Domain**: يحتوي على الكيانات الرئيسية وقواعد العمل الأساسية.
- **MyApp.Application**: يحتوي على الواجهات والتطبيقات لخدمات العمل.
- **MyApp.Persistence**: يحتوي على الكود الخاص بالتعامل مع قاعدة البيانات مثل Repositories.
- **MyApp.Infrastructure**: يمكن أن يتضمن الخدمات الخارجية مثل الـ Email Services.
- **MyApp.WebApi**: المشروع المسؤول عن نشر الـ API للفرونت إند.
- **اختبارات المشروع**: كل طبقة يجب أن تكون لها اختبارات خاصة بها لضمان أداء الكود.

باستخدام هذا التنظيم، ستتمكن من اتباع Onion Architecture بفعالية مع هيكلية منظمة وواضحة تجعل من السهل العمل على المشروع وتوسيع نطاقه.
# Where's to use code
لإنشاء مشروع تسجيل دخول باستخدام `national_number` و `LoginType` كمعايير من قاعدة البيانات، يمكنك اتباع هذه الخطوات التفصيلية. سنقوم بتكوين المشروع باستخدام .NET مع بنية تقليدية مع مجلدات منظمة، وسنقوم باستخدام SQL Server للوصول إلى البيانات.

### 1. إعداد المشروع والفولدر استراكشر
- افتح Visual Studio وأنشئ مشروعًا جديدًا من نوع **ASP.NET Core Web API**.
- اختر اسم المشروع (مثل `SSOLoginAPI`)، واضغط **Create**.
  
### 2. إعداد بنية المجلدات في المشروع
نحن هنا نتبع هيكلية تقليدية لمشروع API مع التركيز على الفصل بين الطبقات.

1. الـ**Entities**: يحتوي على الكائنات الأساسية (Models) التي تمثل البيانات.
2. الـ**Data**: يحتوي على إعدادات الاتصال بقاعدة البيانات ووحدة العمل (Unit of Work) إن لزم.
3. الـ**Services**: يشمل الخدمات التي تتعامل مع قواعد البيانات وتطبيق المنطق.
4. الـ**Controllers**: لإضافة مسارات (Endpoints) API التي تتعامل مع الطلبات الخارجية.

ستكون بنية المجلدات النهائية كالتالي:
   - `SSOLoginAPI`
      - **Controllers**
      - **Entities**
      - **Data**
      - **Services**

### 3. إعداد `AppUser` الكيان المخصص في **Entities**
أنشئ كلاس جديدًا باسم `AppUser` داخل مجلد `Entities` لتمثيل مستخدم التطبيق.
```csharp
using Microsoft.AspNetCore.Identity;

namespace SSOLoginAPI.Entities
{
    public class AppUser : IdentityUser
    {
        public string NationalNumber { get; set; }
        public string LoginType { get; set; }
    }
}
```

### 4. إعداد **Data** الطبقة للاتصال بقاعدة البيانات
داخل مجلد `Data`، أنشئ ملف `ApplicationDbContext.cs` وقم بتحديثه ليشمل `AppUser` ويتصل بقاعدة البيانات.

```csharp
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore;
using SSOLoginAPI.Entities;

namespace SSOLoginAPI.Data
{
    public class ApplicationDbContext : IdentityDbContext<AppUser>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) {}

        protected override void OnModelCreating(ModelBuilder builder)
        {
            base.OnModelCreating(builder);
        }
    }
}
```

ثم اضف الاتصال بقاعدة البيانات في `appsettings.json`:
```json
"ConnectionStrings": {
  "DefaultConnection": "Server=.;Database=YourDatabaseName;Trusted_Connection=True;"
}
```

وتحديث `Program.cs` أو `Startup.cs` لإضافة `ApplicationDbContext`:
```csharp
services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
```

### 5. إعداد **Service** لكتابة منطق تسجيل الدخول
في مجلد `Services`، أضف كلاس جديدًا `AuthService.cs` للتعامل مع تسجيل الدخول باستخدام `national_number` و `LoginType`.

```csharp
using Microsoft.Data.SqlClient;
using System.Threading.Tasks;
using SSOLoginAPI.Entities;
using Microsoft.EntityFrameworkCore;

namespace SSOLoginAPI.Services
{
    public class AuthService
    {
        private readonly ApplicationDbContext _context;

        public AuthService(ApplicationDbContext context)
        {
            _context = context;
        }

        public async Task<AppUser> GetUserByNationalNumberAndLoginTypeAsync(string nationalNumber, string loginType)
        {
            return await _context.Users
                .FirstOrDefaultAsync(u => u.NationalNumber == nationalNumber && u.LoginType == loginType);
        }
    }
}
```

### 6. إعداد **Controller** لمسار تسجيل الدخول
أضف `AuthController.cs` داخل `Controllers` لإنشاء API Endpoint لتسجيل الدخول.

```csharp
using Microsoft.AspNetCore.Mvc;
using SSOLoginAPI.Services;
using System.Threading.Tasks;

namespace SSOLoginAPI.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class AuthController : ControllerBase
    {
        private readonly AuthService _authService;

        public AuthController(AuthService authService)
        {
            _authService = authService;
        }

        [HttpPost("login")]
        public async Task<IActionResult> Login(string nationalNumber, string loginType)
        {
            var user = await _authService.GetUserByNationalNumberAndLoginTypeAsync(nationalNumber, loginType);
            if (user == null)
            {
                return Unauthorized("Invalid national number or login type.");
            }
            return Ok("Login successful");
        }
    }
}
```

### 7. تهيئة قاعدة البيانات وبدء التشغيل
- قم بإنشاء قاعدة بيانات SQL Server وتأكد من تشغيل الـ Connection string في `appsettings.json`.
- تأكد من تنفيذ الأوامر الخاصة بإنشاء الجداول من خلال `dotnet ef migrations add InitialCreate` و `dotnet ef database update`.

### 8. اختبار تسجيل الدخول
بمجرد إعداد الـ API، يمكنك استخدام أداة مثل **Postman** لاختبار مسار `login` عن طريق إرسال طلب POST إلى `http://localhost:5000/api/Auth/login` مع المعايير `nationalNumber` و `loginType`.

بهذه الطريقة، سيكون لديك API جاهز للعمل مع تسجيل الدخول باستخدام المعايير المطلوبة

### تحديث `AuthService` لاستخدام `SqlCommand` مع `Stored Procedure`

في `AuthService.cs`، بدلًا من استخدام `Entity Framework`، سنستخدم `SqlCommand` للوصول المباشر إلى قاعدة البيانات وتشغيل الإجراء المخزن.

1. عدل `AuthService.cs` ليشمل الكود التالي:

```csharp
public class AuthService
{
   private readonly string _connectionString;

   public AuthService(IConfiguration configuration)
   {
	   _connectionString = configuration.GetConnectionString("DefaultConnection");
   }

   public async Task<AppUser> GetUserByNationalNumberAndLoginTypeAsync(string nationalNumber, string loginType)
   {
	   AppUser user = null;

	   using (SqlConnection con = new SqlConnection(_connectionString))
	   {
		   using (SqlCommand cmd = new SqlCommand("Portal_Get_SSO_DATA", con))
		   {
			   cmd.CommandType = CommandType.StoredProcedure;

			   cmd.Parameters.Add(new SqlParameter("@national_number", nationalNumber));
			   cmd.Parameters.Add(new SqlParameter("@LoginType", loginType));

			   con.Open();

			   using (SqlDataReader reader = await cmd.ExecuteReaderAsync())
			   {
				   if (reader.Read())
				   {
					   user = new AppUser
					   {
						   Id = reader["Id"].ToString(),
						   UserName = reader["UserName"].ToString(),
						   NationalNumber = reader["NationalNumber"].ToString(),
						   LoginType = reader["LoginType"].ToString()
						   // أضف أي حقول إضافية حسب حاجتك
					   };
				   }
			   }
		   }
	   }

	   return user;
   }
}
```

2. هنا:
   - `Portal_Get_SSO_DATA` هو اسم الإجراء المخزن في قاعدة البيانات، ويتم تمرير `@national_number` و`@LoginType` كمعاملات كما في الكود الذي أرسلته.
   - بعد تنفيذ الإجراء المخزن، نقوم بقراءة النتائج باستخدام `SqlDataReader`، ونقوم بتهيئة كائن `AppUser` استنادًا إلى البيانات المسترجعة.

### تعديل AuthController للتحقق من المستخدم

داخل `AuthController`، يمكنك التحقق من تسجيل الدخول بنفس الطريقة:

```csharp
[HttpPost("login")]
public async Task<IActionResult> Login(string nationalNumber, string loginType)
{
    var user = await _authService.GetUserByNationalNumberAndLoginTypeAsync(nationalNumber, loginType);
    if (user == null)
    {
        return Unauthorized("Invalid national number or login type.");
    }
    return Ok("Login successful");
}
```

بهذه الطريقة، استخدمنا الكود الذي أرسلته للوصول المباشر إلى قاعدة البيانات باستخدام `SqlCommand`.