---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-24
---
![[Pasted image 20241024015031.png]]
### 1. Data Annotations
الـ**Data Annotations** هي **Attributes** تُضاف مباشرة إلى **الكلاسات أو خصائص الكائنات** (مثل الأعمدة)، وتوفر طريقة سريعة وبسيطة لتعريف القواعد الخاصة بقاعدة البيانات.

#### **أمثلة على Data Annotations:**
```csharp
public class Employee
{
    [Key]
    public int Id { get; set; }

    [Required]
    [MaxLength(50)]
    public string Name { get; set; }

    [Range(1000, 5000)]
    public decimal Salary { get; set; }
}
```

#### **مميزات Data Annotations:**
- **سهولة الاستخدام:** يمكن إضافتها بسرعة فوق الخصائص مباشرة.
- **مناسبة للتطبيقات البسيطة:** حيث تكون القواعد محدودة ولا تحتاج لتعريفات معقدة.
- **وضوح التوثيق:** تجعل الكود أكثر وضوحًا وتشرح المتطلبات مباشرة ضمن النموذج (Model).

#### **عيوب Data Annotations:**
- **محدودية القابلية للتخصيص:** لا تدعم جميع الإمكانيات المتقدمة التي يوفرها EF Core.
- **تؤثر على صيانة الكود:** وضع التقييدات مباشرة في الكلاس يمكن أن يجعل الكود مزدحمًا ويصعّب صيانته إذا كبرت قاعدة البيانات أو زاد التعقيد.

---

### 2. Fluent API
الـ**Fluent API** تعتمد على **سلاسل من الاستدعاءات (Method Chaining)** تُستخدم داخل ملف `DbContext` لتحديد إعدادات قاعدة البيانات والعلاقات بين الجداول بطريقة برمجية.

#### **مثال على Fluent API:**
```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Employee>()
            .HasKey(e => e.Id);

        modelBuilder.Entity<Employee>()
            .Property(e => e.Name)
            .IsRequired()
            .HasMaxLength(50);

        modelBuilder.Entity<Employee>()
            .Property(e => e.Salary)
            .HasRange(1000, 5000);
    }
}
```

#### **مميزات Fluent API:**
- **مرونة عالية:** يدعم تخصيص العلاقات والإعدادات المعقدة مثل **Inheritance** أو **Composite Keys** التي لا يمكن التعامل معها بسهولة باستخدام Data Annotations.
- **فصل التهيئة عن النموذج:** يجعل الكود أكثر تنظيمًا وقابلية للصيانة من خلال فصل القواعد في ملف التهيئة (`OnModelCreating`).
- **يعمل على جميع الإعدادات:** يمكن استخدامه لتحديد كل شيء في الـ Entity Framework Core، مما يجعله الطريقة الأكثر شمولًا.

#### **عيوب Fluent API:**
- **تعقيد أكبر:** يمكن أن يصبح الكود معقدًا وصعب القراءة، خاصة في المشاريع الكبيرة.
- **يحتاج وقتًا أطول في الكتابة:** مقارنة بـ Data Annotations التي توفر حلولًا سريعة للقيود الأساسية.

---

### متى تستخدم كل طريقة؟

#### **استخدم Data Annotations عندما:**
- **المشروع بسيط** ولا يحتاج إلى تخصيصات معقدة.
- تريد طريقة سريعة لتعريف القواعد وتوثيقها ضمن النموذج نفسه.
- تحتاج فقط إلى قيود أساسية مثل `Required`، `MaxLength`، و`Key`.

#### **استخدم Fluent API عندما:**
- **التطبيق معقد** ويتطلب تخصيصات متقدمة (مثل **Composite Keys** أو **Table Splitting**).
- تريد **فصل التهيئة عن الكود** الأساسي لجعل النموذج أنظف وأسهل في الصيانة.
- تحتاج إلى التحكم الكامل في كيفية تعامل Entity Framework مع العلاقات والبيانات.

---

### الخلاصة:
- الـ**Data Annotations** سهلة وسريعة، لكنها محدودة.
- الـ**Fluent API** توفر مرونة عالية وتدعم تخصيصات معقدة، لكنها تحتاج جهدًا أكبر.  

في المشاريع الكبيرة أو التي تتطلب تخصيصات متقدمة، يُفضل استخدام **Fluent API**، بينما يمكن الاعتماد على **Data Annotations** في المشاريع الصغيرة التي لا تحتاج إلى تعقيد.