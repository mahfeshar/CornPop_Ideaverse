---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-23
---
### معنى كلمة **Migration** في سياق Entity Framework

الـ **Migration** تعني عملية **إدارة التغييرات** التي تحدث على **هيكل قاعدة البيانات**. 
بعبارة بسيطة، عندما تقوم بتعديل أي شيء في الكود مثل إضافة **كلاس جديد**، حذف حقل، أو تغيير اسم عمود، فإن هذه التغييرات يجب أن تُطبق على قاعدة البيانات حتى تتطابق مع الكود الذي تكتبه. هنا يأتي دور **Migration**.

---

#### ما الذي يحدث خلال Migration؟
1. **تعريف التغييرات في الكود**: أي تعديل في **Domain Models** (الكلاسات التي تمثل الجداول).
2. **إنشاء Migration**: تقوم **Entity Framework** بإنشاء ملف Migration يحتوي على أكواد لإنشاء أو تعديل الجداول، وإضافة أو حذف أعمدة.
3. **تنفيذ Migration**: يتم تطبيق هذه التغييرات على قاعدة البيانات عن طريق أمر مثل `update-database`، حيث يتم تحديث قاعدة البيانات لتتطابق مع الكود الجديد.

---

#### أنواع التعديلات التي يمكن أن تنفذها Migration:
- **إضافة جدول جديد**.
- **تعديل هيكل جدول موجود** (مثل إضافة أو حذف أعمدة).
- **إنشاء علاقات بين الجداول** (مثل إضافة مفتاح أجنبي Foreign Key).
- **حذف جداول أو أعمدة** لم تعد مستخدمة.

---

#### أهمية Migration
- **تتبع التغييرات**: يمكن لـ Entity Framework تسجيل جميع التغييرات التي تحدث على قاعدة البيانات بمرور الوقت، مما يسهل **إدارة النسخ** المختلفة من قاعدة البيانات.
- **إتاحة الرجوع للخلف**: باستخدام مفهوم `down` في Migration، يمكنك بسهولة التراجع عن أي تعديل حدث إذا ظهرت مشكلة بعد تطبيقه.
- **تحسين التوافق**: يضمن أن التغييرات في الكود تنعكس مباشرة في قاعدة البيانات، مما يقلل الأخطاء الناتجة عن اختلاف الهيكل بين الكود والـ Database.

---

#### خلاصة
الـ **Migration** هو أسلوب فعال لإدارة التغييرات في قواعد البيانات وضمان التزامن بينها وبين الكود. بدونه، سيكون على المطورين تعديل الجداول يدويًا، مما يزيد من احتمال حدوث أخطاء.
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

### 2. **إنشاء الكلاس الذي يمثل جدول في قاعدة البيانات**  
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

### 3. **توضيح دور Entity Framework**  
- إذا لم تكن قاعدة البيانات موجودة بالفعل، تقوم **Entity Framework** بإنشائها.
- في حالة وجودها، تتحقق EF من **الاختلافات** بين الكلاسات (Domain Models) والجداول في قاعدة البيانات. 
  إذا وُجدت تغييرات، يتم إنشاء **Migration** لتعكس هذه التغييرات.

---

### 4. **كيفية عمل Migration**
- افتح **Package Manager Console** ونفّذ الأمر التالي لإنشاء أول Migration:
  ```bash
  add-migration InitialCreate
  ```
- عند الإنشاء الأول، قد تكون الـ Migration فارغة لأننا لم نُعرّف الكلاسات كجداول في الـ **DbContext** بعد.

---

### 5. **توضيح وظائف `up` و`down` في Migration**  
- الـ`up`: يحدد التغييرات التي سيتم تطبيقها على قاعدة البيانات، مثل **إنشاء جدول جديد**.
- الـ`down`: يعمل عكس `up`، مثل **حذف الجدول**، مما يسهل الرجوع إلى أي Migration سابقة عند الحاجة.

```cs
public partial class InitialCreate : Migration
{
    protected override void Up(MigrationBuilder migrationBuilder)
    {
        migrationBuilder.CreateTable(
            name: "Employees",
            columns: table => new
            {
                Id = table.Column<int>(type: "int", nullable: false)
                    .Annotation("SqlServer:Identity", "1, 1"),
                Name = table.Column<string>(type: "nvarchar(max)", nullable: false)
            },
            constraints: table =>
            {
                table.PrimaryKey("PK_Employees", x => x.Id);
            });
    }

    protected override void Down(MigrationBuilder migrationBuilder)
    {
        migrationBuilder.DropTable(
            name: "Employees");
    }
}
```
---

### 6. **ربط الكلاس بـ `ApplicationDbContext`**  
- نعرّف الـ Employee كـ **Domain Model** داخل الـ `DbContext` ليتم التعامل معه كجدول في قاعدة البيانات.

```cs
public class ApplicationDbContext : DbContext
{
	// HERE
    public DbSet<Employee> Employees { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("Server=.;Database=EmployeeManagementDB;Trusted_Connection=True;");
    }
}
```

---

### 7. **التأكد من الـ Migration**  
- قبل تنفيذ الـ Migration على قاعدة البيانات، راجع التغييرات للتأكد من أنها صحيحة.

---

### 8. **إزالة Migration عند الحاجة**  
- إذا احتجت لإزالة Migration قمت بإنشائها:
  ```bash
  Remove-Migration
  ```

---

### 9. **تحديث قاعدة البيانات**  
- لتنفيذ التغييرات على قاعدة البيانات، استخدم الأمر التالي:
  ```bash
  update-database
  ```
- عند فتح **SQL Server** بعد التنفيذ، ستجد:
  - **جدول للـ Employees** يحتوي على الأعمدة التي عرّفناها في الكلاس.
  - **جدول Migration History** الذي يحتوي على تاريخ كل التغييرات التي تمت على قاعدة البيانات.

![[Pasted image 20241023102408.png]]

---

### 10. **ما هو Migration History؟**  
- الـ**Migration History** هو جدول يقوم **Entity Framework** بإنشائه تلقائيًا لتتبع جميع التعديلات التي تمت على قاعدة البيانات.  
- هذا الجدول يسجل كل **Migration** تم تطبيقها، مما يساعد في إدارة التحديثات والرجوع إلى النسخ السابقة عند الحاجة.

---
