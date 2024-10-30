## DbContext
هنعمل أول حاجة الـ DbContext بتاعنا وقولنا هنحطه في الـ Repository Layer

هننزل الـ Packages بقا اللي قولنا عليها زي ما قولنا في ال [[EF Add DbContext and ConnectionString]]

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