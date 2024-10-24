---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-24
---

### إزاي نربط الكلاسات بقاعدة البيانات في Entity Framework Core
- مش أي **كلاس** تحطه في فولدر **Models** هيعتبره EF (Entity Framework) جزء من قاعدة البيانات.  
- علشان EF يتعامل مع الكلاس على إنه **Table** في الـ **Database**، لازم تفهم الـ `ApplicationDbContext` بتاعك إن الكلاس ده **Domain Model**.  

### طرق تعريف الكلاسات كـ Domain Models:

#### 1. الطريقة التقليدية: استخدام `DbSet`
- في الطريقة دي، بنضيف الكلاس اللي عايزين نربطه بقاعدة البيانات جوه الـ `DbContext` كـ **`DbSet`**.

```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Post> Posts { get; set; }
}
```
- كده EF فهم إن **Post** عبارة عن **Table**، ولما تعمل Migration، هيعرف يعمل جدول اسمه **Posts**.

---

#### 2. استخدام Navigation Properties لفهم العلاقات تلقائيًا
- الـ**Navigation Properties** بتحدد **العلاقات** بين الكلاسات (مثل علاقة واحد-ل-كتير بين Blog و Post).  
- حتى لو ما ضفتش الكلاس في `DbContext` كـ **`DbSet`**، طالما في **Navigation Properties**، الـEF هيفهم إن الكلاسات دي مرتبطة ببعض.
- لازم واحد منهم يكون معموله `DbSet` أو معروف للـ Database
```csharp
public class Post
{
    public int Id { get; set; }
    public string Title { get; set; }
    public string Content { get; set; }

    // Navigation Property
    public Blog Blog { get; set; }
}

public class Blog
{
    public int Id { get; set; }
    public string Name { get; set; }

    // Navigation Property
    public List<Post> Posts { get; set; }
}
```
- في المثال ده، EF هيفهم إن في علاقة **One-to-Many** بين Blog و Post، وهيضيف **Foreign Key** تلقائيًا.

##### الـMigration الناتج:
```csharp
migrationBuilder.CreateTable(
    name: "Posts",
    columns: table => new
    {
        Id = table.Column<int>(nullable: false)
                   .Annotation("SqlServer:Identity", "1, 1"),
        Title = table.Column<string>(nullable: true),
        Content = table.Column<string>(nullable: true),
        BlogId = table.Column<int>(nullable: false)
    },
    constraints: table =>
    {
        table.PrimaryKey("PK_Posts", x => x.Id);
        table.ForeignKey(
            name: "FK_Posts_Blogs_BlogId",
            column: x => x.BlogId,
            principalTable: "Blogs",
            principalColumn: "Id",
            onDelete: ReferentialAction.Cascade);
    });
```
- الـ**Foreign Key**: EF هيعمل **BlogId** كـ Foreign Key في جدول Posts.  
- الـ**OnDelete: Cascade**: لو اتشال Blog، هيتشال كل الـ Posts المرتبطة بيه.
	- الأحسن انك تعملها Restrict

---

#### 3. الطريقة التالتة: استخدام modelBuilder في DbContext
- لو مش عايز تضيف الكلاس كـ **DbSet**، ممكن تضيفه بشكل مباشر باستخدام `modelBuilder`.
```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<AuditEntry>();
}
```
- هنا، EF هيعمل **Table** للكلاس `AuditEntry` من غير ما تضيفه كـ DbSet.

---

### الخلاصة:
- الـ**DbSet**: الطريقة التقليدية والمباشرة لإضافة الجداول في EF.
- الـ**Navigation Properties**: تفهم EF العلاقات بين الكلاسات من غير ما تضيف DbSet لكل كلاس.
- الـ**modelBuilder**: مفيد في المشاريع الكبيرة لتحديد الكيانات مباشرة في الـ `OnModelCreating`. 

- **متى تستخدم كل طريقة؟**  
  - لو المشروع بسيط، استخدم **DbSet** عشان يبقى الكود واضح وسهل.  
  - لو عايز تبعد التهيئة عن الكود الرئيسي، استخدم **Navigation Properties** أو `modelBuilder` لتنظيم الكود بشكل أفضل.