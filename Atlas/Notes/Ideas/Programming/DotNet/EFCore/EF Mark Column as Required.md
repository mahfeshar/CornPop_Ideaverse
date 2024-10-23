---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-24
---

اتكلمنا عن الـ [[EF DataAnnotations vs FluentApi]]
### 1. استخدام `Required` مع Data Annotations
- الـ**Data Annotations** تُستخدم بإضافة **Attributes** مباشرة فوق الحقول أو الخصائص (Properties) في الكلاس. 
- عند استخدام `Required`، يحدد هذا الـ Attribute أن **الخاصية لا يمكن أن تحتوي على قيمة فارغة (null)**. 
- في حالة محاولة إدخال قيمة فارغة، سيتسبب ذلك في **خطأ أثناء الحفظ في قاعدة البيانات**.

#### مثال على Data Annotations:
```csharp
public class Employee
{
    [Key]
    public int Id { get; set; }

    [Required]
    public string Name { get; set; }
}
```
- هنا، عند محاولة إضافة **Employee** بدون اسم، سيقوم **Entity Framework** برفض الإدخال لأن الخاصية `Name` تم تقييدها بـ `Required`.

---

### 2. استخدام `Required` مع Fluent API
- في **Fluent API**، يتم تحديد القواعد باستخدام **Method Chaining** داخل الـ `DbContext`.  
- إذا كنت تريد جعل الحقل `Required` باستخدام **Fluent API** بدلًا من **Data Annotations**، يمكنك ذلك عن طريق استدعاء `IsRequired()`.

#### مثال على Fluent API:
```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Employee>()
            .Property(e => e.Name)
            .IsRequired();
    }
}
```
- الـ`IsRequired()` يحدد أن الحقل `Name` لا يمكن أن يكون فارغًا (null) تمامًا مثل استخدام `Required` في Data Annotations.

---

### 3. الفرق بين الطريقتين
1. **Data Annotations**:
   - مباشرة وسهلة الاستخدام، لكنها قد تجعل الكود مزدحمًا عندما تكون هناك الكثير من القيود.
   - مناسبة إذا كنت تريد قواعد بسيطة ومحدودة في النموذج نفسه.

2. **Fluent API**:
   - تمنحك مرونة أكبر، خاصة في التطبيقات المعقدة التي تتطلب **علاقات** أو **تخصيصات متقدمة**.
   - **تُفصل التهيئة** في مكان آخر، مما يجعل النموذج (Model) نظيفًا وأكثر قابلية للصيانة.

---

### 4. كيفية فصل إعدادات Fluent API في ملف منفصل
- في المشاريع الكبيرة، يُفضل أحيانًا **فصل إعدادات الكيانات** عن الـ `DbContext` لجعل الكود أكثر تنظيمًا.

#### خطوات فصل التهيئة في ملف مستقل:
1. أنشئ **ملف جديد** لكل Entity، مثلًا:  
   `EmployeeEntityTypeConfiguration.cs`
2. اجعل هذا الملف **يطبق واجهة IEntityTypeConfiguration**.

##### **الكود:**
```csharp
using Microsoft.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore.Metadata.Builders;

public class EmployeeConfiguration : IEntityTypeConfiguration<Employee>
{
    public void Configure(EntityTypeBuilder<Employee> builder)
    {
        builder.Property(e => e.Name)
               .IsRequired()
               .HasMaxLength(50);  // إضافة قيود إضافية مثل الطول الأقصى
    }
}
```

3. في **`DbContext`**، استدعِ إعدادات التهيئة:
```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.ApplyConfiguration(new EmployeeConfiguration());
    }
}
```

#### طرق أخرى للإستدعاء
بجانب الطريقة التقليدية لتعريف إعدادات Fluent API داخل الـ `DbContext`، هناك **طريقتان إضافيتان** لتنظيم التهيئة بشكل أفضل:

---

##### **الطريقة 1: إنشاء كائن من التهيئة باستخدام `new`**
- يمكنك إنشاء **ملف تهيئة مستقل** لكل Entity. ثم في `DbContext`، تستدعي كل إعداد باستخدام `new` لإنشاء كائن من التهيئة.  
- هذه الطريقة **تنظم الكود**، مما يجعل التهيئة لكل Entity مفصولة في ملفاتها الخاصة.

   ```csharp
   public class ApplicationDbContext : DbContext
   {
       public DbSet<Employee> Employees { get; set; }

       protected override void OnModelCreating(ModelBuilder modelBuilder)
       {
           modelBuilder.ApplyConfiguration(new EmployeeConfiguration());
       }
   }
   ```
---

##### **الطريقة 2: استخدام `ApplyConfigurationsFromAssembly`**
- هذه الطريقة **تقوم بتحميل كل ملفات التهيئة تلقائيًا** من التجميعة (Assembly) التي تحتوي على جميع إعدادات الـ Entities، مما يوفر الوقت ويقلل الأخطاء.
   ```csharp
   public class ApplicationDbContext : DbContext
   {
       public DbSet<Employee> Employees { get; set; }

       protected override void OnModelCreating(ModelBuilder modelBuilder)
       {
           modelBuilder.ApplyConfigurationsFromAssembly(typeof(ApplicationDbContext).Assembly);
       }
   }
   ```
- هذه الطريقة مفيدة **في المشاريع الكبيرة**، حيث تحتاج إلى تطبيق إعدادات كثيرة وتجنب نسيان إضافة بعضها.

---

##### **مقارنة بين الطريقتين:**
| **الطريقة**                         | **متى تستخدمها؟** |
|--------------------------------------|--------------------|
| **new من ملف التهيئة**               | عندما تريد **تحكمًا يدويًا** في استدعاء التهيئات. |
| **ApplyConfigurationsFromAssembly** | عندما تريد **تطبيق جميع التهيئات تلقائيًا** لتقليل التكرار والأخطاء. |

---

##### **الخلاصة:**
- **الطريقة الأولى** باستخدام `new` توفر تحكمًا أكبر وتساعد في **استدعاء التهيئات يدويًا**، وهي مناسبة في المشاريع الصغيرة.
- **الطريقة الثانية** باستخدام `ApplyConfigurationsFromAssembly` تجعل المشروع **أكثر تنظيمًا وقابلية للصيانة**، خاصة في المشاريع الكبيرة حيث يوجد عدد كبير من الكيانات والإعدادات.
---