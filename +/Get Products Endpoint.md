---
up:
  - "[[Asp DotNet Core Web API]]"
  - "[[Asp DotNet Core]]"
related: 
created: 2024-11-14
---
### كود `GetProducts` Endpoint

عشان توصل للـ `GetProducts`، بتروح على `/api/Products` زي ما قلت. 
الكود بيكون كالتالي:

```csharp
[HttpGet]
public async Task<IActionResult> GetProducts()
{
    var products = await _productsRepo.GetAllAsync();

    // الطريقة الأولى: رجعنا الـ products على هيئة Json
    JsonResult result = new JsonResult(products);
    result.StatusCode = 200;
    // لو شيلت سطر الكود دا مش هيرجع ستيتس كود
    return result;
}
```
#### الحل الثاني باستخدام `OkObjectResult`

لو عايز تتفادى ضبط الـ Status Code يدوي، تقدر تستخدم `OkObjectResult` اللي بترجع الـ Status Code كـ 200 بشكل تلقائي:

```csharp
[HttpGet]
public async Task<IActionResult> GetProducts()
{
    var products = await _productsRepo.GetAllAsync();

    // الطريقة الثانية: باستخدام `OkObjectResult`
    OkObjectResult result = new OkObjectResult(products);
    return result;
}
```
#### استخدام `Ok` Helper Method
أحسن طريقة هي استخدام الـ Helper Method `Ok()`، اللي بترجع برضو الـ Status Code كـ 200 بشكل تلقائي ومباشر:

```csharp
[HttpGet]
public async Task<IActionResult> GetProducts()
{
    var products = await _productsRepo.GetAllAsync();
    
    // الطريقة الثالثة: باستخدام Helper Method `Ok`
    return Ok(products);
}
```

---

> **ملاحظة:** الـ `Ok` Helper Method بتسهل الشغل جدًا لأنها بتختصر استخدام الـ Special Classes زي `OkObjectResult` وبتخلي الكود أنظف وأبسط.

---

### المشكلة
لما بتستخدم `Task<IActionResult>`، مش بيديك الـ Swagger الشكل المحدد للـ Response، وده بيسبب مشكلة لما تحب تعرض شكل الداتا المتوقع لكل API Endpoint في Swagger. 

لو حددت إن الدالة ترجع `IEnumerable<Product>`، هيبان شكل الـ Response، لكن كده بتقيد الـ Response بأن يكون دايمًا من نوع `IEnumerable<Product>`، وده مش عملي، خصوصًا لو عايز ترجع أنواع مختلفة من الـ Status Codes زي `NotFound` لما المنتج مش موجود، أو `BadRequest` في حالة حدوث خطأ.

### الحل باستخدام `ActionResult<T>`

بدل ما تستخدم `IActionResult`، الحل الأفضل هنا هو استخدام الكلاس `ActionResult` بنوع Generic، زي كده:

```csharp
Task<ActionResult<IEnumerable<Product>>>
```

### ليه `ActionResult<T>` هو الخيار الأنسب؟

1. **دعم أنواع متعددة من الـ Responses**: 
   - باستخدام `ActionResult<T>`, تقدر ترجع `Ok(products)` لما يكون عندك بيانات، أو `NotFound()` لو مش موجودة، وده بيدي مرونة أكتر في أنواع الـ Responses اللي ممكن ترجعها.

2. **تحديد شكل الـ Response في Swagger**:
   - لما تستخدم `ActionResult<IEnumerable<Product>>`، هيظهر في Swagger شكل الداتا المتوقع اللي من نوع `IEnumerable<Product>`. يعني لو حد شاف الـ API، هيكون عارف الـ Response المتوقع، وده بيسهل فهم API للأشخاص اللي هيستخدموها.

3. **المرونة في التعامل مع الحالات المختلفة**:
   - زي ما قلت، تقدر ترجع أنواع مختلفة زي `Ok`, `NotFound`, `BadRequest`، مع إنك بتحدد نوع الـ Data المتوقع في نفس الوقت.

### مثال كامل على `GetProducts` باستخدام `ActionResult`

```csharp
[HttpGet]
public async Task<ActionResult<IEnumerable<Product>>> GetProducts()
{
    var products = await _productsRepo.GetAllAsync();
    
    if (products == null || !products.Any())
    {
        return NotFound("No products available.");
    }

    return Ok(products);
}
```

### نقاط إضافية:

- **لما ترجع `NotFound()` أو `Ok()`**: بـ `ActionResult<T>`، تقدر تتعامل مع أنواع مختلفة من النتائج بدون ما تفقد مرونة نوع الـ Response.

- **تحسين تجربة Swagger**: بـ `ActionResult<T>`، هيبان نوع الداتا اللي هيرجع، وده بيدي وثائق أكتر وضوحًا لأي حد بيشوف الـ API في Swagger.

### ملخص

استخدام `Task<ActionResult<IEnumerable<Product>>>` بدل `Task<IActionResult>` بيدي مرونة أكتر في أنواع الـ Responses اللي ممكن ترجعها، وبيحسن من توثيق الـ API في Swagger، ويخليك تستفيد من أفضل مميزات ASP.NET Core في التحكم بالـ Status Codes.

---

### مشكلة الـ Related Data في Swagger

لما بنرجع البيانات، بنلاحظ إن الـ Related Data زي `Category` و `Brand` بيكونوا `null` في الـ Response، لأنهم عبارة عن **Navigational Properties**، وبشكل افتراضي مش بيتم تحميلهم مع البيانات الأساسية. عشان نحملهم، عندنا 3 طرق:

1. **Explicit Loading**: تحميل البيانات يدويًا عند الحاجة.
2. **Eager Loading**: تحميل البيانات دفعة واحدة مع الكيان الرئيسي.
3. **Lazy Loading**: تحميل البيانات تلقائيًا عند الوصول للخاصية.

> هنا هنستثني **Explicit Loading**، وهنركز على **Lazy Loading** و**Eager Loading**.

---

### 1. Lazy Loading

#### تعريف Lazy Loading
الـ Lazy Loading هو أسلوب لتحميل البيانات المرتبطة فقط عند الحاجة إليها، وده بيساعد في تقليل كمية البيانات المحملة، وبالتالي تحسين الأداء في بعض الحالات.

#### كيفية تفعيل Lazy Loading

1. **إضافة الـ Proxies Package**:
   - نستخدم الأمر التالي لتثبيت الحزمة:
     ```shell
     dotnet add package Microsoft.EntityFrameworkCore.Proxies
     ```

2. **تفعيل الـ Lazy Loading Proxies في الـ DbContext**:
   - داخل ملف `DbContext`، بنضيف تفعيل للـ Lazy Loading عن طريق `OnConfiguring` أو في `ConfigureServices`:
     ```csharp
     optionsBuilder.UseLazyLoadingProxies();
     ```

3. **تحديد الـ Navigational Properties كـ `virtual`**:
   - كل الـ Navigational Properties لازم تكون `virtual` عشان الـ Lazy Loading تشتغل بشكل صحيح. مثال:
     ```csharp
     public class Product
     {
         public int Id { get; set; }
         public string Name { get; set; }

         public virtual Category Category { get; set; }
         public virtual Brand Brand { get; set; }
     }
     ```

#### متى نستخدم Lazy Loading؟
- **لو البيانات المترابطة مش مطلوبة دائمًا**: بيساعد في تقليل كمية البيانات المحملة.
- **لو بتحتاج مرونة أكبر في الوصول للبيانات المرتبطة**.

> **ملاحظة**: في حالة استخدام الـ Lazy Loading، لازم يكون الـ DbContext مفتوح عند الوصول للـ Related Data، لأنك لو قفلته قبل ما تطلب البيانات، هيظهر لك خطأ.

---

### 2. Eager Loading

#### تعريف Eager Loading
الـ Eager Loading هو أسلوب لتحميل البيانات المرتبطة كلها مرة واحدة مع الكيان الرئيسي. بنستخدمه عشان نضمن إن البيانات المرتبطة بتتحمل دفعة واحدة، وده بيساعد في تحسين الأداء لما نحتاج كل البيانات دفعة واحدة.

#### كيفية تفعيل Eager Loading
نستخدم `Include` عشان نحدد الـ Related Data اللي عايزين نحملها مع الـ Query.
#### مثال على Eager Loading في دالة `GetProducts`

```csharp
[HttpGet]
public async Task<ActionResult<IEnumerable<Product>>> GetProducts()
{
    var products = await _productsRepo
        .GetAll()
        .Include(p => p.Category)
        .Include(p => p.Brand)
        .ToListAsync();

    if (!products.Any())
    {
        return NotFound("No products available.");
    }

    return Ok(products);
}
```

#### متى نستخدم Eager Loading؟
- **لو كنت عايز تحمل كل البيانات المرتبطة مرة واحدة**: خصوصًا لو بتحتاجها بشكل مستمر.
- **لتقليل عدد الاستعلامات**: Eager Loading بيحسن الأداء في الحالات اللي فيها بيانات مترابطة كتير.

---

### ملخص

| النوع           | تعريف                                                                                  | متى يُستخدم                                                                 |
|-----------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **Lazy Loading**  | تحميل البيانات المرتبطة فقط عند الوصول إليها                                           | لما تكون البيانات المترابطة مش مطلوبة دائمًا وتحتاج مرونة أكبر                 |
| **Eager Loading** | تحميل كل البيانات المرتبطة دفعة واحدة باستخدام `Include`                             | لما تحتاج كل البيانات المرتبطة مرة واحدة ولتجنب تكرار الاستعلامات             |

باختصار:
- لو عايز البيانات المرتبطة تتحمل تلقائيًا وقت الحاجة، استخدم **Lazy Loading**.
- لو عايز تحمل كل البيانات المرتبطة مرة واحدة، استخدم **Eager Loading** عن طريق `Include`.

---

### إعداد الـ Include في `GenericRepository`

في ملف الـ `GenericRepository`، لما بنتعامل مع نوع محدد زي `Product`، ممكن نحتاج نحمل الـ `Navigational Properties` زي `Brand` و `Category`، فبنستخدم `Include` كالتالي:

```csharp
if (typeof(T) == typeof(Product))
    return await (IEnumerable<T>) _dbContext.Set<Product>()
        .Include(p => p.Brand)
        .Include(p => p.Category)
        .ToListAsync();
```

### لماذا استخدمنا `Include` فقط بدون `ThenInclude`؟

لأن كلا من `Brand` و `Category` هما **Navigational Properties** مباشرة داخل كلاس `Product`. 
- **استخدام `Include`** يكفي لتحميلهم لأنهم موجودين بشكل مباشر في الكلاس.
- **متى نستخدم `ThenInclude`؟** نستخدم `ThenInclude` فقط عندما تكون عندنا علاقة داخل علاقة أخرى. مثلًا، لو كان الـ `Category` موجودًا داخل `Brand` وليس بشكل مباشر في `Product`، كنا هنستخدم `ThenInclude` عشان نصل إلى الـ `Category`.

### هل يتم تنفيذ **Inner Join** عند استخدام `Include`؟

نعم، عند استخدام `Include` لتحميل الـ `Navigational Properties`، الـ Entity Framework Core بينشئ استعلام `INNER JOIN` في الخلفية لجلب البيانات المرتبطة. الاستعلام بيكون مشابه لـ:

```sql
SELECT *
FROM Products
INNER JOIN Brands ON Products.BrandId = Brands.Id
INNER JOIN Categories ON Products.CategoryId = Categories.Id
```

> **ملاحظة**: في حالة لو كانت القيم المرتبطة (مثل `Brand` أو `Category`) بتقبل `null`، بيتم تنفيذ **LEFT JOIN** بدل من `INNER JOIN`، عشان نضمن استرجاع كل المنتجات حتى لو مش مرتبط بيها `Brand` أو `Category`.

### حل المشكلة باستخدام Specification Design Pattern

أفضل حل هنا هو استخدام **Specification Design Pattern** لأنه بيوفر مرونة في تحديد شروط البحث والـ Includes المطلوبة.
- هذا الـ Pattern بيسمح لنا بكتابة الشروط المطلوبة والـ Includes مرة واحدة فقط، وإعادة استخدامها بدون تكرار.
- يساعد في جعل الكود أكتر تنظيمًا وأسهل في الصيانة، لأنه بيجمع الشروط المشتركة في مكان واحد يمكن تطبيقه في عدة أماكن.

باستخدام الـ Specification Pattern، نقدر نحدد الشروط زي `Include` و`Where` بسهولة، ويكون الحل مثالي للـ Queries اللي بتحتاج أكتر من شرط أو شرط معين على نوع معين من البيانات.
## More
