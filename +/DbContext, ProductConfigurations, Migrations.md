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

	public DbSet<Product> 
}
```