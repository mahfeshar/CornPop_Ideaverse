---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-26
---

بشكل افتراضي، أي حقل من نوع `string` بيتعمله ربط في قاعدة البيانات بيكون نوعه `nvarchar(max)`. 
شفنا إزاي نغير النوع لـ `varchar` مع تحديد الطول، لكن هنا هنتعلم إزاي نخلي النوع `nvarchar` ونحدد الطول الأقصى بدون تغيير النوع الافتراضي.

### تحديد Maximum Length باستخدام Data Annotation

لو حبينا نحدد الطول الأقصى بدون تغيير النوع الافتراضي، ممكن نستخدم **Data Annotation** اللي اسمها `MaxLength`. 
الطريقة بسيطة، بنضيف الأنوتيشن على الخصائص في الكلاس ونحدد الرقم اللي يمثل أقصى طول مسموح به للبيانات.

هنا مثال باستخدام `MaxLength` لتحديد أقصى طول للحقل `Url` بـ 200 حرف:

```csharp
[MaxLength(200)]
public string Url { get; set; }
```

لما نعمل `Add-Migration` أو `Update-Database` بعد إضافة الكود ده، هنلاحظ إن العمود `Url` في قاعدة البيانات اتغير من `nvarchar(max)` لـ `nvarchar(200)`.

### استخدام Fluent API لتحديد Maximum Length

لو مش عايز تستخدم الأنوتيشن، تقدر تعمل نفس التعديلات باستخدام **Fluent API**. 
كل اللي عليك تروح لملف `DbContext` وتستخدم `HasMaxLength` لتحديد الطول الأقصى للعمود.

الكود هيكون بالشكل ده:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .HasMaxLength(200);
}
```
