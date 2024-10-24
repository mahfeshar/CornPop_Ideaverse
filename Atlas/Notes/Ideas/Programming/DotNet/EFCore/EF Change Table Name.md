---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-24
---


### 1. باستخدام Data Annotations
- يمكن تغيير **اسم الجدول** عبر **Data Annotations** باستخدام الـ Attribute `[Table]` الذي يُوضع مباشرة فوق الكلاس. 
- هذا الـ Attribute يُخبر Entity Framework أن الكلاس يُمثّل جدولًا معينًا في قاعدة البيانات باسم مخصص.

```csharp
using System.ComponentModel.DataAnnotations.Schema;

[Table("EmployeesInfo")]
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```
  الكود أعلاه يخبر EF Core بأن الجدول الذي يُمثّل كيان `Employee` سيُسمى **EmployeesInfo** بدلًا من الاسم الافتراضي "Employees".

---

### 2. باستخدام Fluent API
- يمكن أيضًا تغيير اسم الجدول باستخدام **Fluent API** داخل دالة `OnModelCreating` الخاصة بـ `DbContext`. 
- هذه الطريقة توفر **مرونة أكبر**، خاصة في المشاريع الكبيرة حيث يتم فصل إعدادات التهيئة.

```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Employee>()
            .ToTable("EmployeesInfo");
    }
}
```
  هنا يتم تحديد اسم الجدول على أنه **EmployeesInfo** بدلًا من الاسم الافتراضي "Employees". هذا التغيير يتم تطبيقه في قاعدة البيانات عند إنشاء الجداول أو تشغيل Migrations.

---

### **الخلاصة**
- إذا كنت تريد **تغيير اسم الجدول بسرعة وسهولة**، استخدم **Data Annotations**.
- إذا كنت تعمل على **مشروع كبير** وتريد تنظيم التهيئة بشكل منفصل عن النموذج، استخدم **Fluent API**.