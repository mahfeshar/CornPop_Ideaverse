---
up:
  - "[[DotNet MOC]]"
related: 
created: 2024-10-15
---
- [[Asp DotNet Core Web API]]
## ASP .NET Core
الـ**ASP.NET Core** ده Framework معمول من مايكروسوفت، وبيُعتبر الجيل الجديد من ASP.NET اللي الناس كانت بتستخدمه زمان. 
الفكرة في ASP.NET Core إنه بيشتغل على أكتر من نظام تشغيل (يعني مش مقتصر على Windows بس، لأ كمان بيشتغل على Linux وmacOS). 
بيتميز إنه أخف وأسرع، وكمان مرن أكتر وبيتيح ليك تعمل تطبيقات ويب قوية وحديثة سواء Web APIs، أو تطبيقات MVC، أو تطبيقات حقيقية شغالة على الـCloud.

### الفرق بين MVC وRazor Pages:
الخرج بيبقا Web site كامل
الفرق بينهم في المعمارية بتاع كل واحد Architecture 
#### MVC
الـ**MVC (Model-View-Controller)**: ده بيكون نوع من التطبيقات اللي بتستخدم أسلوب تقسيم التطبيق لـ 3 أجزاء:
  - الـ**Model**: ده اللي بيكون مسؤول عن البيانات والـ Business Logic بتاع التطبيق.
  - الـ**View**: الجزء اللي بيظهر للـ user (الشاشة اللي بيتفاعل معاها).
  - الـ**Controller**: المسؤول عن الربط بين الـModel والـView، يعني لما الـ user يعمل طلب معين (زي ما يضغط على زرار أو يبعت طلب API)، الـController بياخد الطلب، يعالجه، ويطلع النتيجة المطلوبة.

  الـ MVC شائع جداً لأنه بيسمح بتقسيم المشروع بحيث يبقى سهل تنظيم الكود والصيانة فيما بعد.
#### Razor Pages
- الـ**Razor Pages**: دي طريقة جديدة ظهرت مع ASP.NET Core، وهي مبنية على فكرة الـMVC بس بأسلوب مختلف شويتين.
- الـRazor Pages بتبقى صفحات مستقلة بذاتها وكل صفحة بتتعامل مع الـ UI والـCode الخاص بيها بشكل منفصل، يعني الكود اللي بيتنفذ في نفس الصفحة مش متقسم زي MVC. 
- هي أبسط في المشاريع الصغيرة أو اللي مش محتاجة التعقيد بتاع MVC.

### الـ Web [[API]]:
الخرج هنا بيبقا اسمه **Web Service**: بعمل خدمة ممكن أي حد يوصلها
الـ**Web API** ده بقى حاجة مختلفة عن الـMVC والـRazor Pages. 
الفكرة من الـWeb API إنها بتخليك تعمل API بيقدر أي برنامج تاني يتعامل معاه عن طريق الإنترنت. 
بمعنى تاني، بدل ما تعمل تطبيق ويب بيطلع صفحات HTML زي MVC، لأ، هنا بتبعت بيانات زي JSON (أو حتى XML) لأي client (سواء كان ويب، موبايل، أو أي نظام تاني).

الـWeb API مثالي لو انت عايز تخلي التطبيق بتاعك يتواصل مع تطبيقات تانية (زي الموبايل أبليكيشن أو سيرفر تاني). 
وميزة تانية، إنه خفيف وسريع وبيعتمد على بروتوكول HTTP.

اللي بيستخدمه بنقول عليه Consumer اللي هو الـ Frontend Developer اللي هو بيبني الـ Client-side application

أشهرهم هو الـ [[REST API]] وفيه برضو [[SOAP API]]

مثال بسيط على Web API:
لو بتعمل أبليكيشن بيجيب بيانات الطقس، تقدر تعمل API يطلع بيانات الطقس في صورة JSON، وده يقدر أي client يطلبه زي موبايل أبليكيشن.

#### ازاي بتعمل Web API؟
- بتعمل **Controller** مخصص للـAPI.
- كل Action جوه الـController ده بيبقى Endpoint، يعني كل Action ممكن يتنادى عليه من client عن طريق HTTP request (زي GET, POST, PUT, DELETE).

#### مثال على Web API في ASP.NET Core:
```csharp
[ApiController]
[Route("api/[controller]")]
public class WeatherController : ControllerBase
{
    [HttpGet]
    public IActionResult GetWeather()
    {
        var weatherData = new { Temperature = 25, Condition = "Sunny" };
        return Ok(weatherData);
    }
}
```
في المثال ده، عملنا API بسيطة جداً بتجيب بيانات الطقس (درجة الحرارة وحالة الجو) وتبعتها في شكل JSON لأي client يطلبها عن طريق HTTP GET request.