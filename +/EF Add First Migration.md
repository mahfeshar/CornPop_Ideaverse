---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-23
---

### 1. **تحديد اسم قاعدة البيانات**  
- يُفضل استخدام **اسم المشروع** أو اسم **الكلاس** كاسم لقاعدة البيانات، لتجنب الالتباس. على سبيل المثال: إذا كان اسم المشروع "EmployeeManagementApp"، فقاعدة البيانات يمكن أن تكون بنفس الاسم.
- ودا نغيره في ال Connection string
```cs
@"Data Source=(localdb)\MSSQLLocalDB;
Initial Catalog=EFCore; /* Name Of Database*/
Integrated Security=True;
Trust Server Certificate=False;"
```

---

#### 2. **إنشاء الكلاس الذي يمثل جدول في قاعدة البيانات**  
- الكلاس الذي تقوم بإنشائه يمثل **Table** في قاعدة البيانات. 
- من الأفضل أن يكون **اسم الكلاس مفردًا** (مثل: `Employee`) لأن **Entity Framework** تلقائيًا تنشئ الجدول بصيغة الجمع (مثل: `Employees`).

```cs
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Salary { get; set; }
}
```

---

#### 3. **توضيح دور Entity Framework**  
- إذا لم تكن قاعدة البيانات موجودة بالفعل، تقوم **Entity Framework** بإنشائها.
- في حالة وجودها، تتحقق EF من **الاختلافات** بين الكلاسات (Domain Models) والجداول في قاعدة البيانات. 
  إذا وُجدت تغييرات، يتم إنشاء **Migration** لتعكس هذه التغييرات.

---

#### 4. **كيفية عمل Migration**
- افتح **Package Manager Console** ونفّذ الأمر التالي لإنشاء أول Migration:
  ```bash
  add-migration InitialCreate
  ```
- عند الإنشاء الأول، قد تكون الـ Migration فارغة لأننا لم نُعرّف الكلاسات كجداول في الـ **DbContext** بعد.

---

#### 5. **توضيح وظائف `up` و`down` في Migration**  
- **`up`**: يحدد التغييرات التي سيتم تطبيقها على قاعدة البيانات، مثل **إنشاء جدول جديد**.
- **`down`**: يعمل عكس `up`، مثل **حذف الجدول**، مما يسهل الرجوع إلى أي Migration سابقة عند الحاجة.

---

#### 6. **ربط الكلاس بـ ApplicationDbContext**  
- نعرّف الـ Employee كـ **Domain Model** داخل الـ DbContext ليتم التعامل معه كجدول في قاعدة البيانات.

```cs
public class ApplicationDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("Server=.;Database=EmployeeManagementDB;Trusted_Connection=True;");
    }
}
```

---

#### 7. **التأكد من الـ Migration**  
- قبل تنفيذ الـ Migration على قاعدة البيانات، راجع التغييرات للتأكد من أنها صحيحة.

---

#### 8. **إزالة Migration عند الحاجة**  
- إذا احتجت لإزالة Migration قمت بإنشائها:
  ```bash
  Remove-Migration
  ```

---

#### 9. **تحديث قاعدة البيانات**  
- لتنفيذ التغييرات على قاعدة البيانات، استخدم الأمر التالي:
  ```bash
  update-database
  ```
- عند فتح **SQL Server** بعد التنفيذ، ستجد:
  - **جدول للـ Employees** يحتوي على الأعمدة التي عرّفناها في الكلاس.
  - **جدول Migration History** الذي يحتوي على تاريخ كل التغييرات التي تمت على قاعدة البيانات.

---

#### 10. **ما هو Migration History؟**  
- **Migration History** هو جدول يقوم **Entity Framework** بإنشائه تلقائيًا لتتبع جميع التعديلات التي تمت على قاعدة البيانات.  
- هذا الجدول يسجل كل **Migration** تم تطبيقها، مما يساعد في إدارة التحديثات والرجوع إلى النسخ السابقة عند الحاجة.

---

### الخاتمة  
بهذه الطريقة، تم شرح كيفية إعداد المشروع وربطه بقاعدة البيانات باستخدام **Entity Framework** في .NET 8، بدءًا من تعريف الكلاسات وحتى تنفيذ الـ Migration.
هنغير اسم الـ Database ممكن يبقا لإسم البروجكت بتاعي أو الكلاس

## Table in Database
هعمل كلاس وهو دا اللي هيمثل Table في الـ Database
حاول تخلي اسم الكلاس دا يبقا فردي مثال: `Employee` عشان هي تلقائي بتعمل الـ Table في الـ Database بالجمع `Employees`

لحد دلوقتي معندناش Database اسمها `EFCore` فدا الدور اللي هتعمله الـ Entity Framework:
- هي هتحاول تشوف الـ Database بتاعتك موجودة ولا لا، لو موجودة بيبدأ يشوف ايه الإختلافات اللي حصلت بين الكلاسيز -اللي هي بتمثل الـ Tables الموجودة في الـ DB- ومبين الـ Tables اللي موجودة فعليًا (بتشوف ايه الإختلافات وتعمل Generate Migration للإختلافات اللي حصلت دي)
  ولو مش موجودة بيعملها Creation وبعد كدا يبدأ يضيف الـ Tables اللي انت عملتها

ازاي اعمل Migration بين الأبلكيشن بتاعي والـ DB 
هندخل على ال Package Manager Console
```bash
add-migration InitialCreate
```
هيعمل Migration بس هتبقا فاضية
عندنا اتنين فانكشن واحدة up -> ابديتز اللي هتحصل على الداتا بيز بعد ما غيرت في الدومين موديلز بتاعتك أو في الكلاسيس بتاعتك 
عكسها في ال down -> يعني لو فوق بتعمل Create لل Table تحت بتعمل Drop ليه عشان يبقا سهل بالنسبالك ترجع لأي Migration بسهولة

هتبقا فاضية عشان احنا مقولناش لل ApplicationDbContext ان الـ Employee دا عبارة عن دومين موديل مش كلاس عادي (دومين كلاس) هيبقا Table في الـ DB

عشان أمسح الـ Migration بستخدم:
```bash
Remove-Migration
```

عشان أعرفه ان دا دومين موديل بروح على الـ ApplicationDbContext:
```cs
// prop
public DbSet<Employee> Employees {get; set;}
```
ونعمل ال migration ونقراه دايمًا قبل ما ننفذه عشان نتأكد ان دا اللي عايزينه 
الكود
فيه فرق بين انك تخلي الاسترينج فاضية وانها تبقا ب null

ازاي ننفذه على الـ DB؟
```cs
update-database
```
لو فتحنا ال sql server هنلاقي الداتا بيز اتعملت وفيه اتنين Tables واحد لل Migration history والتاني لل Employees 
اشرح ال history دا