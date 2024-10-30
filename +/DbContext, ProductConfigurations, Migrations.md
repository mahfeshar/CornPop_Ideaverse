## DbContext
هنعمل أول حاجة الـ DbContext بتاعنا وقولنا هنحطه في الـ Repository Layer

هننزل الـ Packages بقا اللي قولنا عليها زي ما قولنا في ال [[EF Add DbContext and ConnectionString]]
ونعمل نفس الـحاجات اللي عملناه هنا [[DNAPI Basic CRUD Operations]]

```cs
public class StoreContext : DbContext
{
	// Constructor: Chaining base 
	protected override void OnConfiguring(DbContextOptionsBuilder options)
	{
		options.UseSqlServer("ConntectionString");
	}
	
	// Tables
}
```

وأروح أحط الـ Connection String في الـ`appsettings.json`
```json
"ConnectionStrings" : {
	"DefaultConnection": "string"
}
```
هيبقا عندي 3 Connection Strings