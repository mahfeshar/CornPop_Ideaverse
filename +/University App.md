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
بما أنك تريد بناء API بسيط لتسجيل الدخول باستخدام اثنين فقط من الخصائص (attributes) ولا تحتاج إلى تعقيد هيكلية Onion، يمكنك تبسيط الهيكلية على النحو التالي:

### هيكلية المشروع

في هذه الحالة، يمكنك وضع الكود مباشرةً في الطبقة الرئيسية للتطبيق. يمكنك تنظيم المشروع بهذه الطريقة البسيطة:

```
MyApp/
│
├── Controllers/              # يحتوي على الـ API Controllers
│   └── AuthController.cs     # Controller خاص بتسجيل الدخول
│
├── Services/                 # يحتوي على الخدمات (مثل التعامل مع قواعد البيانات)
│   └── AuthService.cs        # خدمة التحقق من بيانات تسجيل الدخول
│
├── Data/                     # لإدارة الاتصال بقاعدة البيانات
│   └── DatabaseConnection.cs # لتجهيز الاتصال بقاعدة البيانات
│
└── Models/                   # يحتوي على النماذج (Models) الخاصة ببيانات الدخول
    └── LoginModel.cs         # النموذج الخاص بتسجيل الدخول
```

### توزيع الكود

1. **إنشاء AuthController**:
   هذا هو المكان الذي ستضع فيه الـ API endpoint لاستقبال بيانات تسجيل الدخول.

   ```csharp
   [ApiController]
   [Route("api/[controller]")]
   public class AuthController : ControllerBase
   {
       private readonly AuthService _authService;

       public AuthController(AuthService authService)
       {
           _authService = authService;
       }

       [HttpPost("login")]
       public async Task<IActionResult> Login([FromBody] LoginModel model)
       {
           var user = await _authService.GetSSODataAsync(model.NationalNumber, model.LoginType);
           if (user != null)
           {
               return Ok(user); // نجاح تسجيل الدخول
           }
           return Unauthorized(); // فشل تسجيل الدخول
       }
   }
   ```

2. **إنشاء AuthService**:
   في هذه الخدمة، يمكنك وضع الكود الخاص باستدعاء قاعدة البيانات.

   ```csharp
   public class AuthService
   {
       private readonly SqlConnection _connection;

       public AuthService(SqlConnection connection)
       {
           _connection = connection;
       }

       public async Task<UserData> GetSSODataAsync(string nationalNumber, string loginType)
       {
           var cmd = new SqlCommand("Portal_Get_SSO_DATA", _connection);
           cmd.CommandType = CommandType.StoredProcedure;

           cmd.Parameters.AddWithValue("@national_number", nationalNumber);
           cmd.Parameters.AddWithValue("@LoginType", loginType);

           _connection.Open();

           using (var reader = await cmd.ExecuteReaderAsync())
           {
               if (await reader.ReadAsync())
               {
                   var userData = new UserData
                   {
                       // تعبئة الكائن بالبيانات
                   };
                   return userData;
               }
           }

           _connection.Close();
           return null;
       }
   }
   ```

3. **نموذج LoginModel**:
   يمثل النموذج الذي يحتوي على بيانات تسجيل الدخول.

   ```csharp
   public class LoginModel
   {
       public string NationalNumber { get; set; }
       public string LoginType { get; set; }
   }
   ```

### الملخص

هذه الهيكلية مبسطة وتناسب API يحتوي فقط على ميزة تسجيل الدخول.