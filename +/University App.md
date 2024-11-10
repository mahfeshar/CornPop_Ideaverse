# Code from Abdelmohsen
[university\_script](https://www.mediafire.com/file/lf6b7s0sud60erf/university_script.rar/file)

بتاخد اتنين برامتر وبترجع null لو غلط وبترجع البيانات لو صح

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
# Login
```cs
// The given scenario is to create an API for a university application that handles login functionality using two fields: the national ID number and the user type. I'll break down the implementation of the .NET API for this, using a stored procedure named "Portal_Get_SSO_DATA".

// Project Structure:
// 1. Controllers: Contains API Controllers.
// 2. Models: Defines the data models.
// 3. DTOs: Data Transfer Objects, used for defining request/response formats.
// 4. Services: Contains the business logic for handling login.
// 5. Data: Handles database access logic.

// Here's how to implement this in a .NET API:

// Folder Structure:
// ├── Controllers
// │     └── AuthController.cs
// ├── Models
// │     └── User.cs
// │     └── UserType.cs
// ├── DTOs
// │     └── LoginRequestDto.cs
// │     └── LoginResponseDto.cs
// ├── Services
// │     └── AuthService.cs
// ├── Data
// │     └── AuthServiceDatabase.cs

// Step 1: Create the "Models/User.cs" file.
namespace YourNamespace.Models
{
    public class User
    {
        public string NationalNumber { get; set; }
        public UserType LoginType { get; set; } // Enum to represent user type
    }
}

// Step 1.1: Create "Models/UserType.cs" file.
namespace YourNamespace.Models
{
    public enum UserType
    {
        Faculty = 1,
        BachelorStudent = 2,
        PostgraduateStudent = 3
    }
}

// Step 2: Create "DTOs/LoginRequestDto.cs" file.
namespace YourNamespace.DTOs
{
    public class LoginRequestDto
    {
        public string NationalNumber { get; set; }
        public string UserType { get; set; } // "Faculty", "BachelorStudent", "PostgraduateStudent"
    }
}

// Step 3: Create "DTOs/LoginResponseDto.cs" file.
namespace YourNamespace.DTOs
{
    public class LoginResponseDto
    {
        public bool IsAuthenticated { get; set; }
        public string Message { get; set; }
        public string UserRole { get; set; }
    }
}

// Step 4: Implement "Data/AuthServiceDatabase.cs" class.
using System.Data;
using System.Data.SqlClient;
using YourNamespace.Models;

namespace YourNamespace.Services
{
    public class AuthServiceDatabase
    {
        private readonly string _connectionString;
        
        public AuthServiceDatabase(string connectionString)
        {
            _connectionString = connectionString;
        }

        public DataTable ExecuteStoredProcedure(User user)
        {
            using (SqlConnection con = new SqlConnection(_connectionString))
            using (SqlCommand cmd = new SqlCommand("Portal_Get_SSO_DATA", con))
            {
                cmd.CommandType = CommandType.StoredProcedure;
                cmd.Parameters.Add(new SqlParameter("@national_number", user.NationalNumber));
                cmd.Parameters.Add(new SqlParameter("@LoginType", (int)user.LoginType));

                SqlDataAdapter da = new SqlDataAdapter(cmd);
                DataTable dt = new DataTable();
                da.Fill(dt);
                return dt;
            }
        }
    }
}

// Step 5: Create "Services/AuthService.cs".
using System.Data;
using YourNamespace.Services;
using YourNamespace.DTOs;
using YourNamespace.Models;

namespace YourNamespace.Services
{
    public class AuthService : IAuthService
    {
        private readonly AuthServiceDatabase _database;
        
        public AuthService(AuthServiceDatabase database)
        {
            _database = database;
        }

        public async Task<User> ValidateUserAsync(LoginRequestDto request)
        {
            UserType loginType = request.UserType switch
            {
                "Faculty" => UserType.Faculty,
                "BachelorStudent" => UserType.BachelorStudent,
                "PostgraduateStudent" => UserType.PostgraduateStudent,
                _ => throw new ArgumentException("Invalid user type")
            };

            User user = new User
            {
                NationalNumber = request.NationalNumber,
                LoginType = loginType
            };

            DataTable result = _database.ExecuteStoredProcedure(user);
            if (result.Rows.Count == 0)
            {
                throw new ArgumentException("Invalid national number or user type");
            }
            return await Task.FromResult(user);
        }
    }
}

// Step 6: Create "Controllers/AuthController.cs".
using Microsoft.AspNetCore.Mvc;
using YourNamespace.DTOs;
using YourNamespace.Services;

namespace YourNamespace.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class AuthController : ControllerBase
    {
        private readonly IAuthService _authService;
        
        public AuthController(IAuthService authService)
        {
            _authService = authService;
        }

        [HttpPost("login")]
        public async Task<IActionResult> Login([FromBody] LoginRequestDto request)
        {
            try
            {
                var user = await _authService.ValidateUserAsync(request);
                var response = new LoginResponseDto
                {
                    IsAuthenticated = true,
                    Message = "Login successful",
                    UserRole = request.UserType
                };
                return Ok(response);
            }
            catch (ArgumentException ex)
            {
                return Unauthorized(new LoginResponseDto
                {
                    IsAuthenticated = false,
                    Message = ex.Message
                });
            }
        }
    }
}



// Explanation and Changes Needed in AuthServiceDatabase:
// - Modify the "LoginType" values to be easier to use in the application code.
// - You could add a new table called "UserType" that contains the mapping of "Faculty", "BachelorStudent", "PostgraduateStudent" to their respective integer codes (1, 2, 3).

// Benefits of the Above Structure:
// - DTOs for data transfer help ensure that only the required data is exposed and makes the code cleaner.
// - Centralized service handling makes it easier to test and maintain.
// - AuthServiceDatabase access is kept in a separate file, keeping the service logic and database access concerns separate.

// This approach also makes it very simple to switch to any other form of user authentication in the future.

// Program Run Instructions:
// - Ensure that the necessary packages are installed (e.g., Microsoft.EntityFrameworkCore, System.Data.SqlClient).
// - Set up the database connection string in the appsettings.json file.
// - Register dependencies in the Program.cs file for dependency injection:
//   builder.Services.AddScoped<AuthServiceDatabase>(provider => new AuthServiceDatabase(builder.Configuration.GetConnectionString("DefaultConnection")));
//   builder.Services.AddScoped<IAuthService, AuthService>();
// - Run the project using Visual Studio or the .NET CLI.
// - Use a tool like Postman to test the login endpoint by sending POST requests to "api/auth/login" with the appropriate JSON payload.

// Simple Database Setup:
// 1. Create a local SQL Server database named "UniversityAuthDB".
// 2. Run the following SQL script to create the necessary tables and stored procedure:

/*
CREATE TABLE Users (
    NationalNumber NVARCHAR(50) PRIMARY KEY,
    LoginType INT NOT NULL
);

INSERT INTO Users (NationalNumber, LoginType) VALUES
('123456789', 1), -- Faculty
('987654321', 2), -- Bachelor Student
('456123789', 3); -- Postgraduate Student

CREATE PROCEDURE Portal_Get_SSO_DATA
    @national_number NVARCHAR(50),
    @LoginType INT
AS
BEGIN
    SET NOCOUNT ON;
    SELECT * FROM Users WHERE NationalNumber = @national_number AND LoginType = @LoginType;
END
*/

// Database Connection String Setup:
// - Add the connection string to appsettings.json:
// "ConnectionStrings": {
//     "DefaultConnection": "Server=localhost;Database=UniversityAuthDB;Trusted_Connection=True;"
// }

// Dependency Injection Setup in Program.cs:
// builder.Services.AddScoped<AuthServiceDatabase>(provider => new AuthServiceDatabase(builder.Configuration.GetConnectionString("DefaultConnection")));
// builder.Services.AddScoped<IAuthService, AuthService>();


// Program setup
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.DependencyInjection;
using YourNamespace.Services;

namespace YourNamespace
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var builder = WebApplication.CreateBuilder(args);

            // Add services to the container.
            builder.Services.AddControllers();
            builder.Services.AddEndpointsApiExplorer();
            builder.Services.AddSwaggerGen();

            builder.Services.AddScoped<AuthServiceDatabase>(provider => new AuthServiceDatabase(builder.Configuration.GetConnectionString("DefaultConnection")));
            builder.Services.AddScoped<IAuthService, AuthService>();

            var app = builder.Build();

            // Configure the HTTP request pipeline.
            if (app.Environment.IsDevelopment())
            {
                app.UseSwagger();
                app.UseSwaggerUI();
            }

            app.UseHttpsRedirection();

            app.UseAuthorization();

            app.MapControllers();

            app.Run();
        }
    }
}

// gitignore
# Ignore Visual Studio temporary files, build results, and files generated by popular Visual Studio add-ons.

# User-specific files
*.user
*.suo

# Build results
[Bb]in/
[Oo]bj/

# Rider IDE
.idea/

# VS Code
.vscode/

# git folders
.vs/
appsettings.json
launchSettings.json
TantaUniApp.APIs.http

```