---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-14
---
### Get Product by Id Endpoint

لاسترجاع منتج واحد باستخدام الـ Id، لازم نضيف **segment** في الـ URL يمثل **Id** المنتج. مثال:

```plaintext
/api/Products/{id}
// مثال: /api/Products/1
```
### الكود:
```csharp
[HttpGet("{id}")]
public async Task<ActionResult<Product>> GetProduct(int id)
{
    var product = await _productRepo.GetAsync(id);

    if (product is null)
        return NotFound(new { message = "Not Found", statusCode = 404 });

    return Ok(product);
}
```

### شرح
1. **استخدام segment إضافي للـ Id**: نضيف `{id}` كـ segment في الـ URL لتحديد المنتج المطلوب بوضوح.
2. **التحقق من وجود المنتج**:
   - بنستخدم `GetAsync` لاسترجاع المنتج من الـ repository.
   - لو المنتج مش موجود، بنرجع رسالة **Not Found** مع **Anonymous Class** مؤقتًا يحتوي على `message` و `statusCode` للتوضيح.
### توحيد شكل الـ Errors باستخدام Standard Class
لكل نوع من أنواع الأخطاء، هنعمل **Standard Class** لاحقًا عشان نوحد شكل الأخطاء في الـ API، بحيث يكون عندنا Error Response منظم بدل الـ **Anonymous Class** الحالي.

شكل الـ Error:
```cs
// Before
{
    "type": "https://tools.ietf.org/html/rfc9110#section-15.5.5",
    "title": "Not Found",
    "status": 404,
    "traceId": "00-4072813df9530061e84be25321c00f5c-43dde7e417ff83a6-00"
}

// After
{
    "message": "Not Found",
    "statusCode": 404
}
```
### التعامل مع Null في Brand و Category
بعض القيم المرتبطة زي `Brand` و `Category` ممكن تكون `null`. مؤقتًا، عشان القيم الفارغة متظهرش في الـ JSON الناتج، هنستخدم نفس الحلول اللي استخدمناها سابقًا لتجنب ظهور القيم `null` في الـ Response.

```cs
public async Task<T?> GetAsync(int id)
{
    if(typeof(T) == typeof(Product))
    {
        return await _dbContext.Set<Product>()
        .Where(P => P.ID == id)
        .Include(P => P.Brand)
        .Include(P => P.Category)
        .FirstOrDefaultAsync() 
        as T;
    }
    return await _dbContext.Set<T>().FindAsync(id);
}
```