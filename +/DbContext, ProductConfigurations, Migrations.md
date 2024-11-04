---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-04
---

## DbContext
### Store Context
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
	}
}
```
والطريقة اللي فوق دي مشكلتها انها مبتستخدمش الـ [[DNAPI Dependency Injection]]
عندنا طريقة تانية بنستخدم بيها الـ DI
![[DNAPI Basic CRUD Operations#**ApplicationDbContext.cs**|DbContext]]

### program.cs
وبعد كدا هنروح نضيف الـ AddDbContext بتاعنا في الـ Program
```cs
builder.Services.AddDbContext<ApplicationDbContext>(options =>
options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```
ومتنساش تضيف Reference للـ Project اللي اسمه Repository عشان أقدر أستخدم الـ DbContext

---
### Connection String
وأروح أحط الـ Connection String في الـ`appsettings.json`
```json
"ConnectionStrings" : {
	"DefaultConnection": "string"
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
protected override void OnModelCreating(ModelBuilder modelBuilder) { modelBuilder.ApplyConfiguration(new ProductConfigurations()); modelBuilder.ApplyConfiguration(new ProductBrandConfigurations()); modelBuilder.ApplyConfiguration(new ProductCategoryConfigurations()); }
```
الطريقة الجديدة أسهل
```cs
modelBuilder.ApplyConfigurationsFromAssembly(Assembly.GetExecutingAssembly());
```
ببياخدها من الـ Assembly اللي شغال وبياخد كل اللي وارث من الـ`IEntityTypeConfiguration` وبيستخدم الـ [[Reflection]]