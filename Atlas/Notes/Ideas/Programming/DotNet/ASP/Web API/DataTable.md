---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-10
---

### 1. إيه هو الـ DataTable؟

الـ `DataTable` هو كائن في .NET بيشبه الجدول اللي في قاعدة البيانات. 
بيتيح لك تخزين البيانات في **شكل صفوف وأعمدة** زي جدول قاعدة البيانات تمامًا، لكن في الذاكرة (يعني مش مرتبط بقاعدة البيانات بشكل مباشر بعد ما تملى البيانات فيه).

الـ `DataTable` ممكن يبقى مفيد جدًا لو عايز تخزن بيانات بشكل مؤقت وتتعامل معاها، زي ما بيحصل في التطبيقات اللي بتحتاج تعرض بيانات كتير وتنفذ عمليات عليها من غير ما تحتاج ترجع لقاعدة البيانات كل شوية.

### 2. مكونات الـ DataTable

الـ `DataTable` بيتكون من:
- **أعمدة (Columns)**: دي بتحدد شكل البيانات اللي هتخزنها، زي `Name` أو `Age` أو `Email`، ولكل عمود نوع بيانات (`string`, `int`, `DateTime`، إلخ).
- **صفوف (Rows)**: دي بتخزن البيانات الفعلية اللي بتتضاف للـ `DataTable`. كل صف بيمثل سجل أو Record في الجدول.

### 3. إزاي تنشئ DataTable وتضيف بيانات فيه؟

تعال نشوف إزاي ننشئ `DataTable` ونعمل خطوات بسيطة عشان نضيف فيه بيانات ونشوفها.

#### مثال بسيط:

```csharp
using System;
using System.Data;

public class Program
{
    public static void Main()
    {
        // إنشاء DataTable
        DataTable table = new DataTable("Users");

        // إضافة أعمدة
        table.Columns.Add("UserId", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Email", typeof(string));

        // إضافة صفوف
        table.Rows.Add(1, "Ahmed", "ahmed@example.com");
        table.Rows.Add(2, "Mona", "mona@example.com");
        table.Rows.Add(3, "Hassan", "hassan@example.com");

        // عرض البيانات
        foreach (DataRow row in table.Rows)
        {
            Console.WriteLine($"UserId: {row["UserId"]}, Name: {row["Name"]}, Email: {row["Email"]}");
        }
    }
}
```

#### شرح المثال:

- **إنشاء DataTable**: عملنا `DataTable` جديد اسمه "Users".
- **إضافة أعمدة**: ضفنا أعمدة للـ `DataTable` زي `UserId` و `Name` و `Email`. لاحظ إننا بنحدد نوع كل عمود (زي `int` للـ `UserId` و`string` للـ `Name` و`Email`).
- **إضافة صفوف**: ضفنا بيانات المستخدمين باستخدام `table.Rows.Add()`.
- **عرض البيانات**: استخدمنا `foreach` عشان نعرض كل صف من صفوف البيانات.

### 4. إزاي نستخدم DataTable مع قاعدة البيانات؟

عادة، بنستخدم `DataTable` عشان نخزن البيانات اللي راجعة من استعلام SQL أو `Stored Procedure` ونحتفظ بيها بشكل مؤقت. 
لو بنستخدم **ADO.NET**، ممكن نملى الـ `DataTable` بالبيانات اللي جايه من قاعدة البيانات عن طريق `SqlDataAdapter`.

#### مثال مع `SqlDataAdapter`:

افرض عندك قاعدة بيانات فيها جدول اسمه `Users` وعايز تجيب كل البيانات منه وتحطها في `DataTable`:

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

public class Program
{
    public static void Main()
    {
        string connectionString = "your_connection_string_here";

        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            SqlCommand cmd = new SqlCommand("SELECT * FROM Users", connection);
            SqlDataAdapter adapter = new SqlDataAdapter(cmd);

            DataTable usersTable = new DataTable();
            adapter.Fill(usersTable);

            // عرض البيانات
            foreach (DataRow row in usersTable.Rows)
            {
                Console.WriteLine($"UserId: {row["UserId"]}, Name: {row["Name"]}, Email: {row["Email"]}");
            }
        }
    }
}
```

#### شرح المثال:

- **إنشاء SqlConnection**: بنفتح اتصال بقاعدة البيانات.
- **إنشاء SqlCommand**: بنجهز استعلام SQL عشان نجيب كل البيانات من جدول `Users`.
- **استخدام SqlDataAdapter**: بنستخدم `SqlDataAdapter` مع `SqlCommand` ونعمل `Fill` للـ `DataTable` بالبيانات اللي جايه من الاستعلام.
- **عرض البيانات**: بنعرض البيانات اللي اتخزنت في `DataTable` باستخدام `foreach`.

### 5. العمليات الممكنة على DataTable

بمجرد ما البيانات تبقى موجودة في `DataTable`، ممكن تعمل عليها عمليات زي:

- **التصفية**: ممكن تصفي البيانات باستخدام `Select` عشان تجيب صفوف معينة.
  
  ```csharp
  DataRow[] filteredRows = usersTable.Select("UserId = 1");
  ```

- **التعديل**: تقدر تعدل بيانات معينة في صف معين.

  ```csharp
  usersTable.Rows[0]["Name"] = "Ali";
  ```

- **الحذف**: تقدر تحذف صف من الـ `DataTable`.

  ```csharp
  usersTable.Rows[0].Delete();
  ```

- **الحفظ في قاعدة البيانات**: بعد ما تعمل أي تعديل، ممكن تحفظ التعديلات في قاعدة البيانات لو بتستخدم `SqlDataAdapter`.

### 6. استخدام DataTable في التعامل مع البيانات بشكل مؤقت

لو عندك تطبيق بيشتغل على البيانات بشكل مؤقت أو بيتعامل مع بيانات كتير في الذاكرة، الـ `DataTable` بيبقى مفيد جدًا لأنه بيسهللك تخزين وتعديل وعرض البيانات بشكل مستقل عن قاعدة البيانات. 

### ليه نستخدم DataTable؟

1. **المرونة**: سهل تضيف وتعدل وتحذف بيانات من غير ما تتعامل مع قاعدة البيانات مباشرة.
2. **المؤقتية**: مفيد لو عايز تخزن بيانات بشكل مؤقت وتعمل عليها عمليات.
3. **التكامل مع ADO.NET**: سهل التعامل مع `DataTable` لما بتيجي تملأها ببيانات من قاعدة البيانات باستخدام `SqlDataAdapter`.

الـ `DataTable` بيعتبر كأنك شغال على جدول صغير في الذاكرة تقدر تتلاعب فيه براحتك، وتستخدمه في تطبيقك سواء للعرض أو للمعالجة المؤقتة للبيانات.

### متى تستخدم `DataTable`؟

لو النتيجة اللي بترجع أكتر من صف، أو عايز تخزن البيانات في شكل جدول عشان تعمل عليها عمليات كتير بعد كده، ساعتها `DataTable` ممكن تكون مناسبة.