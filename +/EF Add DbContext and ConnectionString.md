---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-23
---

#### 1. **إنشاء مشروع Console Application**
1. افتح **Visual Studio**.
2. اضغط على **Create a new project**.
3. اختر **Console Application**.
4. حدد **إصدار للمشروع**.
5. أدخل اسم المشروع (مثلاً: `EFConsoleApp`) وحدد مكان حفظه، ثم اضغط **Create**.

---

#### 2. **تنزيل (Packages) المطلوبة**
1. كلك يمين على المشروع في **Solution Explorer**.
2. اختر **Manage NuGet Packages**.
3. في التبويب **Browse**، ابحث عن الحزم التالية وقم بتثبيتها:
   - **`Microsoft.EntityFrameworkCore`**  
   - **`Microsoft.EntityFrameworkCore.Tools`**
   - **`Microsoft.EntityFrameworkCore.SqlServer`**  
4. اضغط **Install** لكل حزمة وانتظر حتى يتم تثبيتها بنجاح.

حل آخر:

```bash
dotnet add package Microsoft.EntityFrameworkCore 
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```


#### 3. **إنشاء الكلاس اللي بيربط المشروع بقاعدة البيانات (DbContext)**
هو عبارة عن حلقة الوصل بين البرنامج بتاعنا والـ Database
1. في المشروع، أنشئ ملف جديد باسم `ApplicationDbContext.cs`.
2. في الملف، اكتب الكود التالي لتعريف الـ `DbContext`
3. كل اللي هنعمله المرادي هنعمل override لميثود مهمة اسمها `OnConfiguring` وبنحط فيها الـ Connection String

   ```csharp
   using Microsoft.EntityFrameworkCore;

   public class ApplicationDbContext : DbContext
   {
       public DbSet<Product> Products { get; set; }

       protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
       {
           // وضع Connection String للاتصال بقاعدة البيانات
           optionsBuilder.UseSqlServer(
               "Server=.;Database=MyDatabase;Trusted_Connection=True;");
       }
   }

   public class Product
   {
       public int Id { get; set; }
       public string Name { get; set; }
       public decimal Price { get; set; }
   }
   ```

---

#### 4. **إضافة Connection String**
- في الـ `ApplicationDbContext`، تم استخدام `UseSqlServer` لتحديد **Connection String**.  
- صيغة الـ **Connection String** بالشكل ده:  
  `"Server=.;Database=MyDatabase;Trusted_Connection=True;"`.

