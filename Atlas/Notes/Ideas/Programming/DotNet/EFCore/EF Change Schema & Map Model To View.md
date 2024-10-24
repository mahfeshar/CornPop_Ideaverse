---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-24
---
#### By Default:  
- في **Entity Framework Core**، الجداول يتم إنشاؤها (By Default)** ضمن **Schema dbo** إذا لم يتم تحديد غير ذلك. 
- يمكننا تغيير الـ Schema أو ربط الكيان (Entity) بـ **View** بدلاً من جدول باستخدام طريقتين: **Data Annotations** و **Fluent API**.

---

### تغيير الـ Schema باستخدام Data Annotations

```csharp
using System.ComponentModel.DataAnnotations.Schema;

[Table("Employees", Schema = "hr")]
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```
- يتم إنشاء جدول باسم **Employees**، لكن بدلاً من الـ Schema الافتراضي `dbo`، سيتم إنشاؤه ضمن الـ Schema `hr`.
- إذا لم تحدد أي **Schema**، يتم افتراضيًا استخدام **`dbo`** في **SQL Server**.

---

### تغيير الـ Schema وربط الكيان بـ View باستخدام Fluent API
```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Employee>()
            .ToTable("Employees", "hr");
    }
}
```
- يتم إنشاء الجدول **Employees** داخل **Schema "hr"**.  
- لو لم يتم تحديد Schema، سيتم افتراضياً استخدام **dbo**.

---
### تغيير الـ Default Schema في Entity Framework Core

إذا كنت تريد أن يكون الـ **Schema الافتراضي** لأي جدول يتم إنشاؤه في **Entity Framework Core** مختلفًا عن `dbo`، يمكنك استخدام **Fluent API** داخل `DbContext` لتحديد الـ Schema الافتراضي.

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.HasDefaultSchema("hr");
}
```

- باستخدام **`HasDefaultSchema`**، يتم تعيين **`hr`** كـ Default Schema بدلاً من **dbo**.
- أي جدول يتم إنشاؤه بعد ذلك سيكون تلقائيًا داخل **Schema hr** ما لم تحدد غير ذلك عند تعريف الجدول. 

---
### ربط Class (Domain Model) بـ View:
```csharp
public class ApplicationDbContext : DbContext
{
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Employee>()
            .ToView("EmployeeView");  // ربط الكيان بـ View
    }
}
```
- هنا يتم ربط الـ **Employee** بــ View اسمه **EmployeeView** بدلاً من جدول.  
- لن يتم إنشاء هذا الكيان في الـ Migrations كجدول، بل سيتم التعامل معه كمصدر بيانات مرتبط بـ View.

---

### **الخلاصة**  
- الـ**By default**، يتم إنشاء الجداول داخل **Schema dbo** في حال لم يتم تحديد Schema آخر.  
- استخدم **Data Annotations** إذا كنت تريد تغيير اسم الجدول أو الـ Schema بشكل سريع ضمن النموذج.  
- استخدم **Fluent API** إذا كنت بحاجة إلى **مرونة أكبر**، مثل ربط الكيانات بـ Views أو فصل التهيئة عن الكود الرئيسي لتحسين الصيانة.