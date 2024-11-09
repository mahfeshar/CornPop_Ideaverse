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