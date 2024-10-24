---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-24
---

يمكن تغيير **اسم العمود** الافتراضي الذي يتم إنشاؤه بناءً على الخصائص (Properties) في الكلاس، وذلك باستخدام إما **Data Annotations** أو **Fluent API**.

---

### 1. تغيير اسم العمود باستخدام Data Annotations
- باستخدام **Data Annotations**، يمكن تحديد اسم مخصص للعمود عن طريق الـ `[Column]` Attribute.

```csharp
using System.ComponentModel.DataAnnotations.Schema;

public class Employee
{
    public int Id { get; set; }

    [Column("FullName")]
    public string Name { get; set; }
}
```
- الخاصية `Name` سيتم تخزينها في قاعدة البيانات باسم العمود **FullName** بدلًا من الاسم الافتراضي `Name`.

---

### 2. تغيير اسم العمود باستخدام Fluent API
- مع **Fluent API**، يمكنك تخصيص أسماء الأعمدة داخل دالة `OnModelCreating` في `DbContext`.
```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Employee>()
            .Property(e => e.Name)
            .HasColumnName("FullName");
    }
}
```
- يتم تغيير اسم العمود الذي يمثل الخاصية `Name` إلى **FullName** في الجدول.

---
