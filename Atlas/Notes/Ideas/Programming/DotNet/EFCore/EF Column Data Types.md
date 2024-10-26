---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-26
---
هنتكلم عن تعديل الـ Data Type للأعمدة (Columns) باستخدام Entity Framework Core بطريقة سهلة وفعّالة عشان تناسب المتطلبات الخاصة بك في قاعدة البيانات.

### تعديل أنواع الأعمدة باستخدام Data Annotation

أول حاجة نقدر نعملها هي تحديد نوع معين للعمود بدل النوع الافتراضي. 
في الـ **Entity Framework Core**، لما بتحدد نوع عمود على إنه `string`، بيتحول أوتوماتيك لبيانات من نوع `nvarchar` في قاعدة البيانات. 
لو حبينا نغيره لـ `varchar` مثلاً، نقدر نعمل دا بسهولة باستخدام **Column Annotation**.

هنا مثال بالكود اللي بيحدد نوع العمود كـ `varchar` ويضيف طول أقصى للبيانات المخزنة فيه:

```csharp
[Column(TypeName = "varchar(200)")]
public string Url { get; set; }
```

في الكود دا، استخدمنا `Column` وحددنا **TypeName** بـ `varchar(200)`، يعني نوع العمود هيكون `varchar` وبيخزن لحد 200 حرف فقط.

### الفرق بين nvarchar و varchar

الـ `nvarchar` بيدعم **الـ Unicode**، عشان كده بيشيل حروف ولغات مختلفة بدون مشاكل، بينما `varchar` بيكون مخصص للحروف القياسية فقط، وبيوفر مساحة أقل في بعض الحالات.

### إضافة عمود جديد بنوع Data Type مختلف

في المثال التاني، أضاف المحاضر عمود جديد اسمه `Rating` بنوع بيانات **decimal**. باستخدام نفس الأسلوب، أضاف `decimal(5,2)`, واللي بيوضح إن العمود هيشيل أرقام بحد أقصى 5 خانات، منهم خانتين عشريتين.

الكود بيكون كالتالي:

```csharp
[Column(TypeName = "decimal(5,2)")]
public decimal Rating { get; set; }
```

### استخدام الـ Fluent API لتعديل الأعمدة

في حال كنت مش عاوز تستخدم الأنوتيشن، تقدر تعمل نفس التعديلات باستخدام الـ **Fluent API** في ملف `DbContext`. 
وهنا الفكرة إنك بتعمل إعدادات الأعمدة داخل `OnModelCreating` بدل ما تكون في الكلاس الرئيسي.

لإضافة الأعمدة بالطريقة دي:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .HasColumnType("varchar(200)");

    modelBuilder.Entity<Blog>()
        .Property(b => b.Rating)
        .HasColumnType("decimal(5,2)");


	// ممكن نعملها على مرة واحدة
	modelBuilder.Entity<Blog>(eb => 
	{
		eb.Property(b => b.Url).HasColumnType("varchar(200)");
		eb.Property(b => b.Rating)
			.HasColumnType("decimal(5,2)");
	});
}
```
