---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-10
---
### الطريقة الأولى: ADO.NET
دي الطريقة اللي بنستخدم فيها **ADO.NET** عشان نتعامل مع الـ **Stored Procedure** بشكل مباشر. هنفتح اتصال بقاعدة البيانات ونعمل استدعاء للـ `Stored Procedure` ونتحكم في كل خطوة بنفسنا. خليني أوريك مثال.

#### مثال باستخدام ADO.NET

افرض عندك **Stored Procedure** في قاعدة البيانات اسمها `GetUserById`، ودي بتاخد معامل واحد هو `@UserId` وبتجيب بيانات المستخدم اللي ليه الـ ID ده.

هنمشي على الخطوات دي:

1. **فتح الاتصال** بقاعدة البيانات باستخدام `SqlConnection`.
2. **إعداد الاستعلام** باستخدام `SqlCommand` وتحديد إن الـ `CommandType` هو `StoredProcedure`.
3. **إضافة المعاملات** (لو في معاملات زي `@UserId` هنا).
4. **تنفيذ الاستعلام** وجلب النتائج في جدول بيانات (DataTable).

#### الكود هيبقى كده:

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

public class DatabaseHelper
{
    private readonly string _connectionString;

    public DatabaseHelper(string connectionString)
    {
        _connectionString = connectionString;
    }

    public DataTable GetUserById(int userId)
    {
        using (SqlConnection connection = new SqlConnection(_connectionString))
        {
            using (SqlCommand cmd = new SqlCommand("GetUserById", connection))
            {
                cmd.CommandType = CommandType.StoredProcedure;

                // إضافة المعامل
                cmd.Parameters.Add(new SqlParameter("@UserId", userId));

                // إعداد جدول البيانات عشان نحط فيه النتايج
                DataTable dt = new DataTable();
                
                try
                {
                    // فتح الاتصال
                    connection.Open();

                    // استخدام SqlDataAdapter عشان نملى البيانات في DataTable
                    using (SqlDataAdapter da = new SqlDataAdapter(cmd))
                    {
                        da.Fill(dt);
                    }
                }
                catch (Exception ex)
                {
                    // لو حصل خطأ
                    Console.WriteLine("An error occurred: " + ex.Message);
                }

                return dt; // رجّع البيانات
            }
        }
    }
}
```

### إيه اللي بيحصل هنا؟
- إحنا بنفتح اتصال بقاعدة البيانات، وبنجهز `SqlCommand` اللي هنستدعي بيه الـ `Stored Procedure`.
- بنحدد إن نوع `CommandType` هو `StoredProcedure` عشان نفهمه إننا بنشغل حاجة موجودة في قاعدة البيانات مش استعلام SQL عادي.
- بنضيف المعامل `@UserId`.
- بنشغل الـ `Stored Procedure` ونحط النتايج في `DataTable`.
- بعد كده، بنرجع `DataTable` عشان نقدر نستخدمه في أي جزء تاني من البرنامج.

---

### الطريقة التانية: Entity Framework (EF)
لو عايز تستخدم **Entity Framework**، دي بتبقى أسهل وبتخليك تتعامل مع البيانات على إنها كائنات (Objects). 
الـ Entity Framework بيسهل عليك تنفيذ `Stored Procedures` بدون ما تكتب كود كتير للتحكم في الاتصال والاستعلامات.

#### مثال باستخدام Entity Framework

خلينا نقول عندك نفس الـ `Stored Procedure` اللي اسمه `GetUserById`، وعايز تجيب بيانات المستخدم عن طريق Entity Framework. هنا هنمشي على خطوتين:

1. **تجهيز موديل (Model)** يمثل بيانات الجدول اللي راجع من `Stored Procedure`، زي `User` هنا.
2. **استخدام دالة FromSqlRaw** عشان تنفذ `Stored Procedure` وتجيب البيانات.

#### الكود هيبقى كده:

##### أول حاجة، هنكتب موديل `User`:

```csharp
public class User
{
    public int UserId { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```

##### تاني حاجة، هنضيف الدالة في `DbContext`:

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<User> Users { get; set; }

    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }

    // دالة لاستدعاء Stored Procedure
    public async Task<List<User>> GetUserByIdAsync(int userId)
    {
        return await Users
            .FromSqlRaw("EXEC GetUserById @UserId = {0}", userId)
            .ToListAsync();
    }
}
```

### إيه اللي بيحصل هنا؟
- بنعمل دالة `GetUserByIdAsync` في `DbContext` بتاعنا.
- بنستخدم `FromSqlRaw` عشان نكتب اسم 
  الـ `Stored Procedure` (`GetUserById`) ونمرر له المعامل `userId`.
- بعدين بنستخدم `ToListAsync` عشان نرجع النتايج في صورة قائمة من كائنات `User` (`List<User>`).

#### استخدام الدالة دي هيبقى كده:

```csharp
public class UserService
{
    private readonly AppDbContext _context;

    public UserService(AppDbContext context)
    {
        _context = context;
    }

    public async Task<List<User>> GetUserById(int userId)
    {
        return await _context.GetUserByIdAsync(userId);
    }
}
```

---

### الفرق بين الطريقتين:

1. الـ**ADO.NET**: بتديك تحكم أكتر، لكن بتحتاج منك كتابة كود أكتر عشان تتعامل مع قاعدة البيانات بشكل مباشر.
2. الـ**Entity Framework**: بتسهل عليك الشغل، وبتتعامل مع البيانات كـ Objects، وبتخليك تكتب كود أقل وتركز على منطق التطبيق بدل ما تركز على تفاصيل الاتصال بقاعدة البيانات.

### باختصار:
- لو عايز **تحكم كامل** وبتحب تعمل كل حاجة بنفسك، استخدم **ADO.NET**.
- لو عايز **شغل أسرع** وتتعامل مع البيانات ككائنات، يبقى **Entity Framework** هي الأنسب ليك.