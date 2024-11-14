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