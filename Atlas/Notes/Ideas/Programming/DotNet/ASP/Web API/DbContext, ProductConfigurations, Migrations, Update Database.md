---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-04
---
## DbContext
### Store Context
العملية دي هتتعمل في الـ **Repository Layer** وهنعمل Folder اسمه Data حتى تنزيل الباكدجات

هنعمل أول حاجة الـ DbContext بتاعنا وقولنا هنحطه في الـ Repository Layer

هننزل الـ Packages بقا اللي قولنا عليها زي ما قولنا في ال [[EF Add DbContext and ConnectionString]]
ونعمل نفس الـحاجات اللي عملناه هنا [[DNAPI Basic CRUD Operations]]

```cs
public class StoreContext : DbContext
{
	// Base -> parameter ctor that take DbContextOptions
	public StoreContext():base()
	{
		
	}
	protected override void OnConfiguring(DbContextOptionsBuilder options)
	{
		options.UseSqlServer("ConntectionString");
		// منفعتش معايا
	}
}
```
والطريقة اللي فوق دي مشكلتها انها مبتستخدمش الـ [[DNAPI Dependency Injection]]
عندنا طريقة تانية بنستخدم بيها الـ DI
![[DNAPI Basic CRUD Operations#**ApplicationDbContext.cs**|DbContext]]

### program.cs
وبعد كدا هنروح نضيف الـ `AddDbContext` بتاعنا في الـ Program
```cs
builder.Services.AddDbContext<ApplicationDbContext>(options =>
options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```
ومتنساش تضيف Reference للـ Project اللي اسمه Repository عشان أقدر أستخدم الـ DbContext
بنعملها ب Right Click على الـ Dependencies  

بنحطها تحت `AddSwagger` كدا

---
### Connection String
وأروح أحط الـ Connection String في الـ`appsettings.json`
```json
"ConnectionStrings" : {
	"DefaultConnection": "Server = .; Database = Shary.APIs.Corn; Trusted_Connection = True"
}
```
هيبقا عندي 3 من Connection Strings عشان هيبقا عندي 3 Databases في المشروع

### DbSets
دي زي ما قولنا بتمثل الجداول في المشروع بتاعنا
```cs
public class StoreContext : DbContext
{
	public StoreContext(DbContextOptions<StoreContext> options)
		:base(options)
	{
	}

	public DbSet<Product> Products {get; set;} 
	public DbSet<ProductBrand> ProductBrands {get; set;} 
}
```

### Fluent API
محتاجين نكتب التعديلات اللي عايزين نعملها على الـ Modules بتاعنا
هنعمل Override لـ `OnModelCreating`
```cs
public class StoreContext : DbContext
{
	public StoreContext(DbContextOptions<StoreContext> options)
		:base(options)
	{
	}

	protected override void OnModelCreating(ModelBuilder modelBuilder)
	{
		
	}

	public DbSet<Product> Products {get; set;} 
	public DbSet<ProductBrand> ProductBrands {get; set;} 
}
```

مش محتاج أنادي على الـ `OnModelCreating` بتاع الـ Base اللي هو DbContext عشان مفيهاش `DbSet` فمش هيبقا ليها لازمة

## Product Configuration
هنعمل Folder اسمه Config جوا Folder الـ Data اللي موجودة جوا الـ Repository عشان أحط فيها كل الـ Configurations بتاعنا

![[Pasted image 20241104140906.png]]
بتاخد من الـ Interface اللي اسمه `IEntityTypeConfiguration`
هنبدأ نعمل حاجتين عندنا:
1. الـ Properties كلها بتاعها (تاخد بالك انك تحل مشاكل مثلًا ان عناصر متبقاش NULL)
2. الـ Relationships بينها وبين باقي العناصر (بتحدد نوعها وبعدين بتحدد الـ Foreign key)
```cs
internal class ProductConfigurations : IEntityTypeConfiguration<Product>
{
    public void Configure(EntityTypeBuilder<Product> builder)
    {
        builder.Property(P => P.Name)
            .IsRequired()
            .HasMaxLength(100);

        builder.Property(P => P.Description)
            .IsRequired();

        builder.Property(P => P.PictureUrl)
            .IsRequired();

        builder.Property(P => P.Price)
            .HasColumnType("decimal(18, 2)");

        // Foreign key relationship with Brand
        builder.HasOne(P => P.Brand)
            .WithMany()
            .HasForeignKey(P => P.BrandId);
            //.OnDelete(DeleteBehavior.SetNull); // Uncomment if you want to set null on delete

        // Foreign key relationship with Category
        builder.HasOne(P => P.Category)
            .WithMany()
            .HasForeignKey(P => P.CategoryId);
    }
}
```
ونعمل واحد للـ Brand و Category

دلوقتي هنزود الـ Configuration في الـ `OnModelCreating`
عندنا طريقة قديمة:
```cs
protected override void OnModelCreating(ModelBuilder modelBuilder) 
{ 
	modelBuilder.ApplyConfiguration(new ProductConfigurations()); 
	modelBuilder.ApplyConfiguration(new ProductBrandConfigurations()); 
	modelBuilder.ApplyConfiguration(new ProductCategoryConfigurations()); }
```
الطريقة الجديدة أسهل
```cs
modelBuilder.ApplyConfigurationsFromAssembly(Assembly.GetExecutingAssembly());
```
ببياخدها من الـ Assembly اللي شغال وبياخد كل اللي وارث من الـ`IEntityTypeConfiguration` وبيستخدم الـ [[Reflection]]

## Migrations
اتكلمنا عنها في الـ [[Entity Framework Core]] ,[[EF Add First Migration]]
هنحتاج نعمل الـ Migration في البروجكت بتاع **الـ API اللي فيه الـ Connection string**
**هننزل الـ Package** اللي اسمه `EntityFrameCore.Tools`

لما نيجي نفتح الـ Package Manager هنحدد البروجكت بتاع الـ Repository 
```shell
add-migration "ProductModule" - O Data/Migrations
```

وبعدين نعمل Update-Database
```shell
Update-Database
```
دي بتنفذ سطرين كود كدا انها بتعمل اوبجيكت من الـ DbContext ويمسك الـ Object يقوله `object.Database.Migrate`

---



## Update Database
قولنا طريقة من شوية
بس دي مش أحسن طريقة تتنفذ لأني عايز لما أعمل **run للبرنامج** يعمل Apply Migration لوحده من غير ما أقوله لو مش معمولها Update

هعمل دي عن طريق اني هروح في أول الـ Main وأحط السطرين اللي قولنا عليهم
```cs
StoreContext dbContext = new StoreContext();
await dbContext.Database.MigrateAsync();
```
- بس محتاج هنا أديله Options وأنا لو عملت كدا يدوي هبوظ الـ Dependency Injection
- فأنا محتاج أطلب من الـ CLR يعملي الحوار دا
- ممكن واحد يقولي أعمل Ctor للـ Program نفسه يعملي الـ Object بس دا هيعملي **مشاكل كتير**

- فأنا محتاج أعمل كدا بشكل Explicitly 
- فأنا هطلب بعد ما أعمل Configure بعد الـ DbContext وبعد ما أعمل Build لل App
- محتاج أعمل Create Scope
```cs
var scope = app.Services.CreateScope();
var services = scope.ServiceProvider;
var _dbContext = services.GetRequiredService<StoreContext>();
// Ask CLR for Creating Object from DbContext Explicitly

await _dbContext.Database.MigrateAsync();
```

ولازم بعد ما أخلص شغلي معاه أقفل الـ Scope
وعشان أعمل كدا هستخدم الـ [[Cs Handle Exception#Finally]] لأنها هتتنفذ لما Try تخلص شغلها
```cs
 try
 {
	 var scope = app.Services.CreateScope();
	var services = scope.ServiceProvider;
	var _dbContext = services.GetRequiredService<StoreContext>();
	await _dbContext.Database.MigrateAsync();
 }
 finally 
 {
	 scope.Dispose();
 }
```
او بدل دي هستخدم Using 
```cs
using var scope = app.Services.CreateScope();
var services = scope.ServiceProvider;
var _dbContext = services.GetRequiredService<StoreContext>();
// Ask CLR for Creating Object from DbContext Explicitly

await _dbContext.Database.MigrateAsync();
```

حاجة كمان ان لو حصل مشكلة في الـ Update كدا مش هيعمل Run فهحتاج أعمل الكود في [[Cs Handle Exception#Try … Catch|Try ... Catch]]
```cs
try
{
	await _dbContext.Database.MigrateAsynce();
}
catch (Exception ex)
{
	Console.WriteLine(ex);
}
```
مش هستخدم Console عشان أعرض الـ Error فهستخدم الـ  Logger Factory

### الكود النهائي
```cs
using var scope = app.Services.CreateScope();
var services = scope.ServiceProvider;
var _dbContext = services.GetRequiredService<StoreContext>();

var loggerFactory = services.GerRequiredService<ILoggerFactory>();

try
{
	// Update-Database
	await _dbContext.Database.MigrateAsync(); 
}
catch (Exception ex)
{
	var logger = loggerFactory.CreateLogger<Program>();
	logger.LogError(ex, "an error has been occured during apply the migration");
}
```
خد بالك انت كمان محتاج تعمل ال Program يبقا `async Task`

- الطريقة دي بنستخدمها عشان نعمل Update بشكل مستمر
- كل مرة أشغل البرنامج يعمل Apply لأي Migration عندك
- والموضوع دا مهم لما تيجي تعمل Deploy على Server Production 
- وعشان الـ Data Seeding

## Data Seeding
- Seed => دا البداية اني بعمل داتا مبدأية
- العملية دي بتحصل مرة واحدة في الحياة
  ومرة واحدة للسيرفر 

- اني بحط الداتا موجودة قبل كدا 

### الخطوات
- هنعمل Folder جديد في الفولدر بتاع Data اللي موجود في الـ Repository وأسميه `DataSeeding` 
- نحط فيه ملفات الـ JSON بتاعنا
- جوا فولدر الـ Data هنعمل Helper نسميه `StoreContextSeed` وتبقى `public static`
- نعمل Method اسمها `SeedAsync`
	- ولازم نمررلها الـ Database Context بتاعنا عشان يحطها فيها
- هنبدأ بالـ Category أو الـ Brand وننتهي بالـ Product في الآخر خالص
- هنستخدم الـ `ReadAllText` اللي هي بتفتح الفايل وتاخد الداتا وتقفله 
	- وبنديلها Absolute path لمكان الفايل
- هنستخدم بعد كدا الـ [[JSON]] واتكلمنا قبل كدا عن الـ [[Py json#Deserialization|Deserialize]]

```cs
public static class StoreContextSeed
{
	public async static Task SeedAsync(StoreContext _dbContext)
	{
		// File => String (JSON)
		var brandsData = File.ReadAllText("../Shary.Repository/Data/DataSeed/brands.json");

		// String(JSON) => in-memory objects
		var brands = JsonSerializer.Deserialize<List<ProductBrand>>(brandsData);

		if(brands?.Count() > 0)
		{
			foreach(var brand in brands)
			{
				_dbContext.Set<ProductBrand>().Add(brand);
				// await _dbContext.SaveChangesAsync();
				// نسيف فالأخر خالص أحسن بعد ما يضيف كله
			}
			await _dbContext.SaveChangesAsync();
		}
	}
}
```
لازم نتأكد ان الداتا مش ب null