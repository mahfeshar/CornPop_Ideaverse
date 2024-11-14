عشان أوصلها بنورح على `/api/Products`

```cs
[HttpGet]
public async Task<IActionResult> GetProducts()
{
	var products = await _productsRepo.GetAllAsync();

}
```
ممكن أرجعه على هيئة Json 
```cs
JsonResult result = new JsonResult(products);
return result;
```
بس مش هبقا عارف الـ status code
فعندي حلين اما اني 
```cs
result.StatusCode = 200;
```
اني أحطها يدوي أو اني أستخدم Object من `OkObjectResult` اللي الـ Status code by default بتبقا Ok
```cs
OkObjectResult result = new OkObjectResult(products);
return result;
```
بس أنا مبستخدمش الـ Class ال Special types دي 