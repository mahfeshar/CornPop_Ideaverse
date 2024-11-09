---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-06
---
# Generic Repository
الـ **Generic Repository** هو نمط تصميم (Design Pattern) يُستخدم في تطوير التطبيقات لتقليل تكرار الكود وتحسين مرونة واستدامة التطبيق. 
في إطار العمل زي الـ .NET، بنستخدمه في الطبقة المسؤولة عن التعامل مع قواعد البيانات، خاصة في مشاريع زي **Onion Architecture** أو الهياكل المعيارية.

بيشتغل عن طريق إنشاء واجهة عامة (Generic Interface) بتعرّف العمليات الأساسية اللي بنحتاجها دايمًا للتعامل مع البيانات، زي:

- الـ`Add()`: لإضافة كائن جديد لقاعدة البيانات.
- الـ`GetById()`: عشان نجيب كائن معين حسب الـ ID.
- الـ`GetAll()`: جلب جميع الكائنات من النوع ده.
- الـ`Update()`: لتحديث كائن موجود.
- الـ`Delete()`: لحذف كائن.

الهدف من الـ Generic Repository إنه يوفر لنا واجهة عامة نقدر نستخدمها مع أي نوع كائن بدل ما نكتب كود جديد لكل نوع كائن. 
مثلًا، كده ممكن نعرّفها في كود C# بالشكل ده:

### 1. تعريف الـ Interface:

```csharp
public interface IRepository<T> where T : class
{
    Task<T> GetByIdAsync(int id);
    Task<IEnumerable<T>> GetAllAsync();
    Task AddAsync(T entity);
    Task UpdateAsync(T entity);
    Task DeleteAsync(int id);
}
```

الـ `IRepository` هنا واجهة عامة، ونقدر نستخدمها مع أي كائن من نوع `T`، فيها العمليات الأساسية للتعامل مع البيانات.

### 2. تنفيذ الـ Repository:

```csharp
public class Repository<T> : IRepository<T> where T : class
{
    private readonly DbContext _context;
    private readonly DbSet<T> _dbSet;

    public Repository(DbContext context)
    {
        _context = context;
        _dbSet = context.Set<T>();
    }

    public async Task<T> GetByIdAsync(int id)
    {
        return await _dbSet.FindAsync(id);
    }

    public async Task<IEnumerable<T>> GetAllAsync()
    {
        return await _dbSet.ToListAsync();
    }

    public async Task AddAsync(T entity)
    {
        await _dbSet.AddAsync(entity);
        await _context.SaveChangesAsync();
    }

    public async Task UpdateAsync(T entity)
    {
        _dbSet.Update(entity);
        await _context.SaveChangesAsync();
    }

    public async Task DeleteAsync(int id)
    {
        var entity = await GetByIdAsync(id);
        if (entity != null)
        {
            _dbSet.Remove(entity);
            await _context.SaveChangesAsync();
        }
    }
}
```

في الكود ده، الـ `Repository` بينفذ الـ `IRepository`، وبيستخدم الكائن `DbContext` للتفاعل مع قاعدة البيانات من خلال `DbSet<T>`.

### مميزات الـ Generic Repository:

- **تقليل التكرار**: لأنك تقدر تستخدم نفس الكود مع أنواع مختلفة من الكائنات.
- **إعادة الاستخدام**: بيوفر لك نمط عام للتعامل مع الكيانات المختلفة.
- **مرونة في التغيير**: بتقدر تغير طريقة التخزين أو قاعدة البيانات نفسها بسهولة.

**ملاحظة**: النمط ده مناسب للتطبيقات اللي حجمها متوسط أو كبير لأنه بيساعد في تنظيم الكود.
# In Our Project
احنا هنعمل Product repository بس المفروض قبل يبقا عندي Generic Repository

## Interface
هنحتاج نعمل Interface اسمه `IGenericRepository` وزي ما اتفقنا الـ Interfaces بتتحط في الـ **Core Layer**
فأنا هعمل فولدر وممكن أسميه Repositories أو `Repositories.Contract` ودا الأحسن
وهعمل فولدر كمان لبعد كدا اسمه `Services.Contract` 

```cs
namspace Talabat.Core.Repositories.Contract;
public interface IGenericRepository<T> where T : BaseEntity
{
	// We will make now: 2 methods
	Task<T?> GetAsync(int id);
	Task<IEnumerable<T>> GetAllAsync();
}
```
- لازم تبقا `BaseEntity`
- المفروض بنعمل 5 Signatures لل 5 methods بتاعنا 
  بس احنا هنعمل اتنين بس get, get all لأن مش طبيعي الشخص اللي بيتسوق يعدل أو يضيف أو يحذف

الاتنين دول هيبقوا شغالين Synchronoss فهنستخدم Task وهترجع T أو `IEnumerable` من الـ T

## Class
بعدين نروح في الـ Repository ونضيف الـ Class بتاعنا
```cs
public class GenericRepository<T> : IGenericRepository where T : BaseEntity
{
	private readonly StoreContext _dbContext;
	public GenericRepository(StroreContext dbContext)
	{
		_dbContext = dbContext;
	}
	public Task<IEnumerable<T>> GetAllAsync()
	{
		return await _dbContext.Set<T>().ToListAsync();
	}
	public Task<T?> GetAsync(int id)
	{
		return await _dbContext.Set<T>(),FindAsync(id);
	}
}
```

- لازم برضو نحدد انه الـ T لازم تبقا `BaseEntity` 
- محتاج أستخدم الـ DbContext عشان ترجعلي الداتا دي
- ممكن يبقا عندي Repository تانية وهيبقا فيها Generic Repository تانية وعنده DbContext تانية
- لازم تخلي اللي بتجيب بالـ Id تقبل Nullable لأنها ممكن ترجع Null
- مش هنعمل Product ولا Category ولا Brand ك Repository لأني **مش هضيف فيهم أي حاجة جديدة** انما لو هزود فانكشن ولا حاجة لازم نعمل واحد ويورث من دا