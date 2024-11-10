فيه أكتر من طريقة تقدر تستخدمها للتعامل مع نتائج الـ **Stored Procedure** في .NET، حسب احتياجاتك وحسب الـ **Library** اللي بتستخدمها.
### 1. استخدام [[DataTable]]

بنستخدم فيها `SqlDataAdapter` و `DataTable` عشان نخزن البيانات في جدول داخل الذاكرة. الطريقة دي مناسبة لو عايز تخزن النتائج في صيغة جدولية تقدر تتعامل معها بسهولة، وخصوصًا لو عندك أكتر من صف في النتيجة.

---

### 2. استخدام `DataReader` مع ADO.NET

بدل ما تستخدم `DataTable`، تقدر تستخدم `SqlDataReader` لو عايز تجيب البيانات بشكل أسرع، وده بيفيد لو بتتعامل مع كمية كبيرة من البيانات أو محتاج أداء أعلى. `DataReader` بيقرأ البيانات صف بصف (Row by Row) من قاعدة البيانات من غير ما يخزنها كلها في الذاكرة، فبيكون أسرع وأقل في استهلاك الموارد.

#### مثال:

```csharp
using System.Data;
using System.Data.SqlClient;

public void GetUserById(int userId)
{
    using (SqlConnection connection = new SqlConnection(_connectionString))
    {
        using (SqlCommand cmd = new SqlCommand("GetUserById", connection))
        {
            cmd.CommandType = CommandType.StoredProcedure;
            cmd.Parameters.Add(new SqlParameter("@UserId", userId));

            connection.Open();

            using (SqlDataReader reader = cmd.ExecuteReader())
            {
                while (reader.Read())
                {
                    Console.WriteLine("User ID: " + reader["UserId"]);
                    Console.WriteLine("Name: " + reader["Name"]);
                    Console.WriteLine("Email: " + reader["Email"]);
                }
            }
        }
    }
}
```

في المثال ده، بنستخدم `SqlDataReader` لقراءة البيانات صف بصف من غير ما نخزنها في `DataTable`.

---

### 3. استخدام الـ **Entity Framework** وإرجاع البيانات كـ Objects

لو بتستخدم **Entity Framework**، مش محتاج تخزن النتايج في `DataTable`، تقدر ترجع النتايج على طول كـ List من الكائنات (Objects)، زي ما شفنا في المثال اللي فات باستخدام `FromSqlRaw`. وده بيسهل التعامل مع البيانات بشكل كائنات بدل الجداول.

#### مثال باستخدام Entity Framework:

```csharp
public async Task<List<User>> GetUserByIdAsync(int userId)
{
    return await _context.Users
        .FromSqlRaw("EXEC GetUserById @UserId = {0}", userId)
        .ToListAsync();
}
```

الطريقة دي بترجع `List<User>` على طول، من غير ما نحتاج نخزن النتايج في `DataTable`.

---

### 4. تخزين النتيجة في كائن (Object) مخصص

لو عندك نتيجة بسيطة، ممكن تنشئ كائن مخصص (Custom Object) وتحط فيه النتايج اللي راجعة من `Stored Procedure` بدل `DataTable`. 
الطريقة دي مفيدة لو النتيجة عبارة عن صف واحد أو عدد قليل من الأعمدة.

#### مثال:

```csharp
public class User
{
    public int UserId { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}

public User GetUserById(int userId)
{
    using (SqlConnection connection = new SqlConnection(_connectionString))
    {
        using (SqlCommand cmd = new SqlCommand("GetUserById", connection))
        {
            cmd.CommandType = CommandType.StoredProcedure;
            cmd.Parameters.Add(new SqlParameter("@UserId", userId));

            connection.Open();

            using (SqlDataReader reader = cmd.ExecuteReader())
            {
                if (reader.Read())
                {
                    return new User
                    {
                        UserId = (int)reader["UserId"],
                        Name = reader["Name"].ToString(),
                        Email = reader["Email"].ToString()
                    };
                }
            }
        }
    }

    return null; // في حالة عدم وجود بيانات
}
```

هنا بنرجع كائن `User` مباشرة بدل `DataTable`، وده بيكون مناسب لو بتتعامل مع نتيجة مكونة من صف واحد.

---
### 3. استخدام `ExecuteScalar` لو النتيجة قيمة واحدة

لو الاستعلام أو الـ `Stored Procedure` بيرجع **قيمة واحدة بس** (مثلاً عدد المستخدمين أو قيمة معينة)، ممكن تستخدم `ExecuteScalar` بدل ما تستخدم `DataTable` أو `DataReader`.

#### مثال:
```cs
public int GetUserCount()
{
    using (SqlConnection connection = new SqlConnection(_connectionString))
    {
        SqlCommand cmd = new SqlCommand("SELECT COUNT(*) FROM Users", connection);
        
        connection.Open();
        int userCount = (int)cmd.ExecuteScalar();
        
        return userCount;
    }
}
```
### ملخص

- الـ**DataTable**: مناسب لو عايز تخزن البيانات بشكل جدول وتتعامل مع أكتر من صف في الذاكرة. (**أكتر من صف**)
- الـ**DataReader**: أسرع وأخف على الذاكرة، وبيفيد لما يكون عندك كمية بيانات كبيرة. (**صف واحد - كائن**)
- الـ**Entity Framework**: بيرجع النتايج كـ List من الكائنات مباشرة، وبيسهل التعامل مع البيانات في شكل Object-Oriented.
- الـ **ExecuteScalar**: استخدم `ExecuteScalar` لو النتيجة عبارة عن قيمة واحدة (زي عدد أو قيمة). (قيمة واحدة)
- **كائن مخصص (Custom Object)**: ممكن ترجع كائن مباشرة لو النتيجة صف واحد أو بيانات بسيطة، بدل ما تستخدم `DataTable`.

على حسب احتياجاتك، تقدر تختار الطريقة المناسبة للتعامل مع نتائج الـ **Stored Procedure**.