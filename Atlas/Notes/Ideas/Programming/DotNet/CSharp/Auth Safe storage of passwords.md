---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-15
---
تخزين كلمات المرور (passwords) في قواعد البيانات، التركيز كان على أهمية تأمين كلمات المرور لتجنب حدوث اختراقات للبيانات. 
ووضح إن تخزين كلمات المرور بشكل آمن هو خطوة حيوية جدًا للحفاظ على أمان التطبيق، خصوصًا في حالة تعرض قاعدة البيانات للاختراق.

### 1. أخطر حاجة: تخزين كلمات المرور بـ Clear Text
**تخزين كلمات المرور بالنص الصريح** (Clear Text) هو أسوأ فكرة ممكن تتخيلها. ليه؟ لأن لو حصل اختراق لقاعدة البيانات، كل المعلومات، بما فيها كلمات المرور، هتبقى متاحة للهكرز، وبالتالي هيقدروا يدخلوا على حسابات المستخدمين بكل سهولة. 
في حالة حصول الاختراق ده، المطور هيضطر يبلغ المستخدمين يغيروا كلمات المرور الخاصة بيهم، وده بيكون إحراج وضغط كبير.

![[Pasted image 20241015030044.png]]
### 2. استخدام **[[Hashing]]** لكلمات المرور:
الخيار الثاني اللي وضحه هو استخدام **Hashing**.
فكرة الـ **hashing** هي إننا ناخد كلمة المرور، ونطبق عليها خوارزمية **hash**، والنتيجة النهائية هي إننا نخزن الـ **hash** في قاعدة البيانات بدل كلمة المرور الأصلية. 
الميزة هنا إن **hashing** هو عملية في اتجاه واحد، يعني مينفعش ترجع لكلمة المرور الأصلية من الـ **hash**.

لكن المشكلة مع الـ **hashing** العادي هي إنه لو فيه اتنين من المستخدمين استخدموا نفس كلمة المرور (زي "let me in")، هيكون عندهم نفس **hash**، وده بيخلي الهكرز يقدروا يعرفوا بسهولة إن المستخدمين دول بيستخدموا نفس الباسورد، وبالتالي يخترقوا حساباتهم.

![[Pasted image 20241015030300.png]]
### 3. الحل الأمثل: **Hashing** و **Salting** معًا
عشان نحل المشكلة دي، لازم نستخدم تقنية الـ **Salting**. 
الفكرة هنا إننا نضيف سلسلة عشوائية (salt) مع كلمة المرور قبل ما نطبق عليها خوارزمية الـ **hashing**. 
وده بيضمن إن حتى لو اتنين من المستخدمين استخدموا نفس كلمة المرور، هيكون عندهم **hash** مختلف تمامًا بسبب الـ **salt**.

الـ **salt** ده بيتخزن كمان في قاعدة البيانات بجانب الـ **hash**، وبيتم استخدامه لما المستخدم يسجل الدخول، بحيث نقدر نتحقق إذا كانت كلمة المرور اللي دخلها صح ولا لأ.

![[Pasted image 20241015030503.png]]
#### إزاي نطبق الفكرة دي؟

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

### ليه مش بنستخدم ASP.NET Identity دلوقتي؟
سؤال بيتسأل كتير: ليه مش نستخدم **ASP.NET Identity** اللي بيعمل كل الشغل ده بشكل تلقائي وسهل؟ 
الإجابة ببساطة هي إننا عايزين نفهم ازاي الموضوع بيشتغل من جوه بدل ما نعتمد على حلول جاهزة. 
لما نكتب الكود بنفسنا، هنفهم أكتر إزاي الـ **authentication** بيشتغل، وبعد كده ممكن نستخدم **ASP.NET Identity** لما نكون فهمنا الأساسيات بشكل كويس.

### خلاصة:
التطبيق اللي كتبناه ده يعتبر طريقة مبسطة لتطبيق **authentication** في التطبيقات، لكنه مش الحل النهائي أو الأقوى للأمان في التطبيقات الكبيرة. 
الهدف من الشرح هو إننا نفهم الأساسيات قبل ما ننتقل لحلول أكثر تقدمًا زي **ASP.NET Core Identity** اللي بيعتبر حل شامل وآمن جدًا، ومستخدم في تطبيقات كبيرة وموثوقة.