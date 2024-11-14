---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-14
---
### خطوة 1: إنشاء Controller جديد باسم `ProductsController`

هنفتح فولدر الـ `Controllers` داخل مشروع الـ API، وهنعمل Controller جديد.
هنسميه `ProductsController` وهنختار يكون API من النوع Empty، بحيث يرث من `ControllerBase`.

### خطوة 2: إعداد الـ Route
الـ Route بيكون بشكل افتراضي `api/[controller]`، وده معناه إننا بنقدر نتواصل مع الكنترولر ده من خلال `api/Products`.

### خطوة 3: إنشاء BaseApiController
عشان نتجنب تكرار الـ Route في كل Controller، هنضيف `BaseApiController` اللي هيرث من `ControllerBase`، ونحط فيه الـ Route `api/[controller]` عشان يتطبق على كل الكنترولرز اللي هيرثوا منه.

```csharp
[Route("api/[controller]")]
[ApiController]
public class BaseApiController : ControllerBase
{
    // ممكن إضافة أكواد مشتركة هنا
}
```

> **ملاحظة:** ده مش هو الـ Common Controller؛ يعني مش الهدف منه نحط Endpoints مشتركة، بس هو معمول للتعامل مع الـ Routing بس.

### خطوة 4: إنشاء Endpoints في `ProductsController`

هنضيف اتنين Endpoints في `ProductsController`، واحد بيجيب كل المنتجات (Products) والتاني بيجيب المنتج بالـ ID.

أول حاجة، لازم يبقى عندنا Object من `ProductRepository`، وده ممكن نجيبه من `GenericRepository` باستخدام الـ Constructor Injection.

#### كود `ProductsController` مع Constructor Injection

```csharp
public class ProductsController : BaseApiController
{
    private readonly IGenericRepository<Product> _productsRepo;

    public ProductsController(IGenericRepository<Product> productsRepo)
    {
        _productsRepo = productsRepo;
    }

    // Endpoints
}
```

### خطوة 5: إضافة الـ Dependency Injection في `Program.cs`

في الملف `Program.cs`، هنضيف الـ `GenericRepository` بشكل Scoped لكل الـ Repositories، بحيث لو عملنا Object من Interface معين، الـ DI هيعمل Object من الـ Class المقابل.

#### كود إضافة Scoped لكل Repository

```csharp
builder.Services.AddScoped<IGenericRepository<Product>, GenericRepository<Product>>();

builder.Services.AddScoped<IGenericRepository<ProductBrand>, GenericRepository<ProductBrand>>();

builder.Services.AddScoped<IGenericRepository<ProductCategory>, GenericRepository<ProductCategory>>();
```

#### إضافة Scoped لكل Repositories بشكل عام
لتجنب التكرار لو عندنا كتير من الـ Repositories، هنضيف Generic Repository Injection بشكل عام:

```csharp
builder.Services.AddScoped(typeof(IGenericRepository<>), typeof(GenericRepository<>));
```

---
