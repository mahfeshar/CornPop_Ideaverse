هنشرح مع بعض مفهوم **CRUD Operations** وازاي نطبقها باستخدام **ASP.NET Core**. الكراد أو **CRUD** هو اختصار لـ: 

- **Create** (إنشاء)
- **Read** (قراءة)
- **Update** (تعديل)
- **Delete** (حذف)

ودي العمليات الأساسية اللي بتتم على أي **Entity** في قاعدة البيانات. 
يعني، أي نظام مبني على قواعد بيانات، غالبًا هيحتاج إنه يقدر ينشئ، يقرأ، يعدل، ويحذف بيانات.

---

### تجهيز المشروع وإنشاء قاعدة البيانات  
أول خطوة، بنحتاج ننشئ **SQL Server Database**. 
في الفيديو، تم استخدام **SQL Management Studio** لتسهيل إدارة قاعدة البيانات. 
قمنا بإنشاء **Database** باسم **Products** وإنشاء **Table** بسيط داخله لتخزين بيانات المنتجات. 

#### الـ SQL Script لإنشاء قاعدة البيانات:
```sql
CREATE DATABASE Products;
GO
USE Products;

CREATE TABLE Products (
    Id INT IDENTITY(1,1) PRIMARY KEY,
    Name NVARCHAR(50) NOT NULL, """Unicode"""
    SKU VARCHAR(50) NOT NULL
);
```

- الـ**Id**: المفتاح الأساسي للجدول (Primary Key)، ومُعرف كـ **Identity** بحيث يزيد تلقائيًا.
- الـ**Name**: اسم المنتج.
- الـ**SKU**: معرف المنتج (Stock Keeping Unit).

---

### إعداد المشروع في ASP.NET Core  
في مشروعنا، هنضيف الـ **Entity Framework Core** عبر **NuGet Packages**. 
مكتبة **EF Core** بتسهل التعامل مع قواعد البيانات بشكل مباشر من الكود.

#### تثبيت EF Core:
1. افتح **NuGet Package Manager**، وابحث عن:  
   - `Microsoft.EntityFrameworkCore`
   - `Microsoft.EntityFrameworkCore.SqlServer`

2. اضغط **Install** على المكتبتين، وهيتم تثبيتها في المشروع.

---

### إنشاء الـ Entity والـ DbContext  
الـ **Entity** هي الكلاس اللي بتمثل **Table** في قاعدة البيانات. (Record or row in table)
أما الـ **DbContext** فهو الكلاس اللي بيوصل بين التطبيق وقاعدة البيانات. (ممثل الـ Database)

#### **Product.cs**:
```csharp
public class Product
{
    public required int Id { get; set; }
    public required string Name { get; set; }
    public required string SKU { get; set; }
}
```

#### **ApplicationDbContext.cs**:
```csharp
public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) 
        : base(options) { }

    public DbSet<Product> Products { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Product>().ToTable("Product");
    }
}
```

- لازم يورث من كلاس اسمه `DbContext`
- أول حاجة لازم نعمل override لميثود اسمها `OnModelCreating` ودي بكل بساطة بقوله إن معايا Entities وبعرفه `ToTable` انه هيروح يعدل هناك في الجدول دا
- لو هو هو نفس اسم الـ Entity مش لازم تديله اسم انما لو مختلف لازم تكتب اسم الجدول في الـ DB بالظبط
- لو الـ Primary Key اسمه ID أو اسمه اسم الـ Entity وبعده ID زي `ProuctID` هو تلقائي بيتعرف عليها انما لو مختلف لازم استخدم `HasKey("Id")` واكتب الـ Primary key
- متنساش تعمل empty constructor عشان ميعمليش ايرور ويبقا بياخد `DbContextOptions`

---

### تسجيل الـ DbContext في الـ Dependency Injection Container  
في **Program.cs**، هنضيف الـ **DbContext** ضمن الـ **Services** باستخدام `AddDbContext`.

#### **Program.cs**:
```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddDbContext<ApplicationDbContext>(options => options.UseSqlServer("Server=.;Database=Products;Trusted_Connection=True;"));

builder.Services.AddControllers();
builder.Services.AddSwaggerGen();

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
app.Run();
```

---

### إنشاء Controller يحتوي على CRUD Operations  
هنضيف **ProductController** وهنبني فيه العمليات الأربع (Create, Read, Update, Delete).

#### **ProductController.cs**:
```csharp
[ApiController]
[Route("api/[controller]")]
public class ProductController : ControllerBase
{
    private readonly ApplicationDbContext _context;

    public ProductController(ApplicationDbContext context)
    {
        _context = context;
    }

    [HttpPost]
    public async Task<IActionResult> Create(Product product)
    {
        _context.Products.Add(product);
        await _context.SaveChangesAsync();
        return Ok(product.Id);
    }

    [HttpGet]
    public async Task<IActionResult> GetAll()
    {
        var products = await _context.Products.ToListAsync();
        return Ok(products);
    }

    [HttpGet("{id}")]
    public async Task<IActionResult> GetById(int id)
    {
        var product = await _context.Products.FindAsync(id);
        if (product == null) return NotFound();
        return Ok(product);
    }

    [HttpPut("{id}")]
    public async Task<IActionResult> Update(int id, Product product)
    {
        var existingProduct = await _context.Products.FindAsync(id);
        if (existingProduct == null) return NotFound();

        existingProduct.Name = product.Name;
        existingProduct.SKU = product.SKU;
        await _context.SaveChangesAsync();

        return Ok();
    }

    [HttpDelete("{id}")]
    public async Task<IActionResult> Delete(int id)
    {
        var product = await _context.Products.FindAsync(id);
        if (product == null) return NotFound();

        _context.Products.Remove(product);
        await _context.SaveChangesAsync();

        return Ok();
    }
}
```

---

#### شرح الكود:
- الـ**Create**: يستقبل **Product** جديد ويضيفه لقاعدة البيانات.
- الـ**GetAll**: يسترجع كل المنتجات.
- الـ**GetById**: يسترجع منتج معين بناءً على **Id**.
- الـ**Update**: يعدل بيانات منتج موجود.
- الـ**Delete**: يحذف منتج بناءً على **Id**.

---

### تجربة الـ API باستخدام Swagger  
الـSwagger بيكون جاهز تلقائيًا مع **ASP.NET Core**، وبيسهل عليك تجربة الـ API. 

1. شغل التطبيق، وافتح Swagger من الرابط:  
   `https://localhost:5001/swagger/index.html`

2. جرب العمليات المختلفة (Create, Read, Update, Delete) باستخدام الواجهة التفاعلية.

---

### الخاتمة  
في الفيديو ده، شرحنا بالتفصيل إزاي نبني **CRUD Operations** باستخدام **ASP.NET Core** و**Entity Framework Core**. العملية سهلة وبسيطة، لكنها أساسية لأي تطبيق يعتمد على قواعد بيانات. فهم **CRUD** هيساعدك في بناء تطبيقات قوية ومرنة. 

يا رب يكون الشرح واضح وسهل. ما تنسوش الدعاء لإخواننا في فلسطين، والسلام عليكم ورحمة الله وبركاته.