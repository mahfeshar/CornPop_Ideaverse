---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-15
---

## مقدمة عن الـ Authentication:
في التطبيقات بتحتاج تطبق الـ **authentication**، وده ببساطة يعني إنك تتأكد إن المستخدم اللي بيحاول يدخل للتطبيق هو فعلاً الشخص اللي بيقول إنه هو. 
الأهداف الرئيسية في الجزء ده هي إننا نطبق **basic authentication** ونتعلم إزاي نخزن كلمات المرور (passwords) في قاعدة البيانات (database) بطريقة آمنة.

## التخزين الآمن لكلمات المرور:
لما المستخدمين بيسجلوا أو يعملوا **login**، لازم نفكر إزاي نخزن كلمات المرور بتاعتهم بشكل آمن. 
مينفعش نخزن كلمات المرور كده صريحة (plain text) لأنها هتبقى عرضة للاختراق. 
بدل كده، بنستخدم تقنيات زي **[[Hashing]]** اللي بتحول كلمة المرور لصيغة مش قابلة للرجوع مرة تانية، بحيث لو حصل اختراق، ميبقاش سهل إن حد يطلع على كلمة المرور الفعلية.

## وراثة الأكواد (Inheritance) في C#:
[[Cs Inheritance]]
مفهوم مهم جداً في الـ C# هو **Inheritance** أو "الوراثة". 
الفكرة ببساطة إنك متكررشي نفسك في كتابة الكود، أو زي ما بنقولها في المصطلح البرمجي "Dry"، اللي معناها "Do not repeat yourself". 
بتستخدم **inheritance** عشان لو عندك أكواد متشابهة ممكن تخلي كلاس (class) أساسي (base class) يحتوي على الوظائف المشتركة، والكلاسات التانية (derived classes) ترث منه.

## استخدام الـ Debugger:
جزء تاني مهم في الفيديو هو إزاي نستخدم الـ **debugger** في C# عشان نتابع الكود بتاعنا ونتأكد إنه شغال صح. يعني تقدر تمشي خطوة بخطوة في الكود وتشوف كل خطوة بتحصل إزاي وتفهم لو فيه أي أخطاء بتحصل أثناء تنفيذ الطلبات اللي بتيجي من السيرفر.

## الـ DTOs والـ Validation:
هيتم شرح كمان مفهوم **Data Transfer Objects** أو الـ DTOs، واللي هو ببساطة الكائنات اللي بنبعتها من الـ API للمستخدمين أو بنستقبلها من عندهم. 
ودي طريقة منظمة عشان نبعت البيانات اللي إحنا عاوزين نوصلها من غير ما نعرض تفاصيل كتير.

## الـ validation
الـ **validation** أو "التحقق" هو جزء تاني مهم جداً، يعني قبل ما تقبل أي بيانات من المستخدم لازم تتحقق إنها مظبوطة ومتوافقة مع اللي انت عايزه عشان ميبقاش فيه مشاكل لاحقاً.

## توكن الـ JWT:
التوثيق هيتم باستخدام **JSON Web Tokens** أو الـ **JWT**. 
ودي عبارة عن طريقة للتوثيق بنستخدمها لما بيكون مفيش اتصال دائم مع المستخدم، يعني بعد ما المستخدم يسجل الدخول بنبعتله **token**، وكل ما يحتاج يعمل طلب من الـ API يبعت الـ token ده.

## الـ Services والـ Middleware:
في الفيديو كمان بيتم التطرق لمفهوم الـ **services**، ودي عبارة عن أجزاء من الكود بنستخدمها عشان نقدم خدمات معينة في التطبيق، زي توثيق المستخدمين مثلاً. كمان فيه حاجة تانية اسمها **middleware**، ودي بتشتغل زي مرحلة تمر بيها الطلبات اللي جاية للسيرفر وتقدر من خلالها تعمل تعديلات أو تحقق في الطلبات قبل ما توصل للجزء الأساسي اللي بيعالجها.

## طرق لتجنب تكرار الكود:
زي ما ذكرنا الوراثة (inheritance)، فيه كمان حاجة اسمها **extension methods**. 
دي بتساعدك إنك تضيف وظائف جديدة للأكواد الموجودة من غير ما تحتاج تغير الكود الأصلي، وبالتالي بتقلل من تكرار الكود.

## خطوات البدء:
أخيراً، قبل ما تبدأ أي مشروع، لازم تحدد المتطلبات. 
زي في مثالنا اللي بنتكلم فيه عن تطبيق اجتماعي (social dating app)، المتطلبات بتكون إن المستخدمين لازم يقدروا يسجلوا الدخول، يسجلوا حسابات جديدة، يشوفوا مستخدمين تانيين، ويقدروا يبعثوا رسائل خاصة. 

وأول حاجة بتبدأ بيها هي بناء كائن الـ user، وبعد كده بتبني باقي التطبيق حواليه.

## الكود:
في الفيديو كان فيه مثال بسيط عن تخزين الـ passwords بشكل آمن، ممكن يكون كود شبه ده:

```csharp
public class User
{
    public int Id { get; set; }
    public string Username { get; set; }
    public byte[] PasswordHash { get; set; }
    public byte[] PasswordSalt { get; set; }

    public void CreatePasswordHash(string password, out byte[] passwordHash, out byte[] passwordSalt)
    {
        using (var hmac = new System.Security.Cryptography.HMACSHA512())
        {
            passwordSalt = hmac.Key;
            passwordHash = hmac.ComputeHash(System.Text.Encoding.UTF8.GetBytes(password));
        }
    }

    public bool VerifyPasswordHash(string password, byte[] storedHash, byte[] storedSalt)
    {
        using (var hmac = new System.Security.Cryptography.HMACSHA512(storedSalt))
        {
            var computedHash = hmac.ComputeHash(System.Text.Encoding.UTF8.GetBytes(password));
            for (int i = 0; i < computedHash.Length; i++)
            {
                if (computedHash[i] != storedHash[i]) return false;
            }
        }
        return true;
    }
}
```

الكود ده بيوريك إزاي تخزن كلمة المرور كـ **hash** وتتحقق منها لما المستخدم يحاول يعمل تسجيل دخول.