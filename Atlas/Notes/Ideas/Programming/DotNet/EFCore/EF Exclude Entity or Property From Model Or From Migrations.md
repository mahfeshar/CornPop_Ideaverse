---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-24
---
في بعض الحالات، قد تحتاج إلى **استبعاد كائن أو خاصية** من قاعدة البيانات، سواء كان ذلك لمنع تخزينه، أو للتعامل معه فقط داخل التطبيق. 
هناك طريقتان رئيسيتان لفعل ذلك: **Data Annotations** باستخدام `[NotMapped]`، أو **Fluent API** باستخدام `Ignore` أو `ExcludeFromMigrations`. 

---

### 1. استثناء Properties باستخدام `[NotMapped]`

- الـ`[NotMapped]` هو **Attribute** ضمن **Data Annotations** يتم استخدامه لإخبار **EF Core** بعدم تضمين **خاصية معينة** في الجداول عند إنشاء قاعدة البيانات أو إجراء Migrations.
```csharp
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }

    [NotMapped]  // هذه الخاصية لن تُخزن في الجدول
    public int Age { get; set; }
}
```
- في المثال السابق، يتم استثناء الخاصية `Age` من التخزين في الجدول، حتى لو كانت مستخدمة في التطبيق.
- ممكن تستخدمها على الـ Navigation Properties فبالتالي ميظهر الـ Entity كلها

#### **متى تستخدم `[NotMapped]`؟**
- **الخصائص المحسوبة** مثل `TotalPrice` التي يتم حسابها في التطبيق.
- **البيانات المؤقتة** التي لا تحتاج إلى تخزينها في قاعدة البيانات.

#### **خاصية محسوبة كمثال:**
```csharp
public class Order
{
    public int Id { get; set; }
    public decimal UnitPrice { get; set; }
    public int Quantity { get; set; }

    [NotMapped]
    public decimal TotalPrice => UnitPrice * Quantity;
}
```
- في هذا المثال، `TotalPrice` يتم حسابها بناءً على البيانات الموجودة، لكن لا يتم تخزينها كعمود في قاعدة البيانات.

---

### 2. استثناء Properties أو Entities باستخدام Fluent API
باستخدام **Fluent API**، لديك تحكم أكبر، حيث يمكنك استبعاد خصائص أو كيانات مباشرة داخل `OnModelCreating`.
#### استبعاد Property باستخدام `Ignore()`
- يمكن استثناء خصائص معينة من التتبع والـ Migrations باستخدام Fluent API من خلال استدعاء `Ignore()` داخل `OnModelCreating`.

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Employee>()
                .Ignore(e => e.Age);
}
```
- هذا الكود يستثني الخاصية `Age` من التتبع، مما يعني أنها لن تُدرج في الجدول.

#### استثناء Entity باستخدام `ExcludeFromMigrations()`
- أحيانًا تريد أن يكون الكيان جزءًا من الـ Model في التطبيق، لكن بدون تضمينه في الـ Migrations.  
- باستخدام **`ExcludeFromMigrations()`**، يتم استثناء الكيان من أي جداول أو Migrations تُنشأ في قاعدة البيانات.

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .ToTable("Blogs", b => b.ExcludeFromMigrations());
}
```
- في المثال السابق، يتم استثناء **Blog** من أي Migration، حتى لو تم التعامل معه داخل الكود.

#### مقارنة بين Ignore و `ExcludeFromMigrations`:

| **`Ignore()`**                         | **`ExcludeFromMigrations()`**               |
|-----------------------------------------|---------------------------------------------|
| يستبعد الكيان تمامًا من الـ Model و Migrations. | يستبعد الكيان فقط من الـ Migrations، لكن يمكن استخدامه في الكود. |
| لا يمكن التعامل مع الكيان في الكود ضمن EF.   | يمكن التعامل معه في الكود دون إضافته للـ Database. |

---

### الخلاصة:
- الـ`[NotMapped]` يُستخدم لاستثناء **الخصائص الفردية** التي لا تحتاج إلى تخزينها في قاعدة البيانات.
- الـ`Ignore()` يستثني الكيانات أو الخصائص بالكامل من EF Core.
- الـ`ExcludeFromMigrations()` يسمح لك باستخدام الكيان داخل الكود، لكنه يمنع إضافته إلى **الـ Database** عبر الـ Migrations.

---