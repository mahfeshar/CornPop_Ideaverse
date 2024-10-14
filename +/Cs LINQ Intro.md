---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-14
---
## مقدمة عن LINQ في C#

أول حاجة لازم نكون عارفين إن **LINQ** هي اختصار لـ **Language Integrated Query**، ودي عبارة عن طريقة أو أسلوب بتقدر من خلاله تتعامل مع **data collections** زي **List** و**Arrays** وغيرها باستخدام صيغة شبه الـ SQL اللي بنستعملها في قواعد البيانات.
بتتعامل مع الـ [[Cs Enumerable]]

### أهمية LINQ

لو سبق ليك التعامل مع قواعد بيانات، فأكيد استخدمت [[SQL Server MOC|SQL]] في استعلام البيانات. 
الفكرة الأساسية في **LINQ** هي إنها بتقدملك نفس المرونة اللي بتحصل عليها مع قواعد البيانات، ولكن على مستوى الأكواد والـ **collections** اللي بتتعامل معها في تطبيقك. 
زي ما تقدر تسأل قاعدة بيانات عن الموظفين اللي مرتباتهم أعلى من حد معين أو الطلاب اللي درجاتهم أكتر من مستوى معين، تقدر تعمل نفس الحاجة لكن في الكود مباشرةً.

### مميزات LINQ

من المميزات اللي بتقدمها **LINQ**:
- **Filtering**: زي إنك تجيب الأرقام الأكبر من 5 من قائمة أرقام.
- **Sorting**: ترتيب البيانات.
- **Grouping**: تجميع البيانات بناءً على شروط معينة.
- **Joining**: دمج البيانات من أكتر من مصدر.

### مقدمة بسيطة عن LINQ Syntax

الفكرة هنا هي إننا عندنا **List** من الأرقام، وعايزين نجيب الأرقام اللي أكبر من 5.

#### الطريقة التقليدية باستخدام For Loop:
```cs
List<int> numbers = new List<int> { 1, 2, 3, 6, 7, 8, 10 };
List<int> result = new List<int>();

foreach (int number in numbers)
{
    if (number > 5)
    {
        result.Add(number);
    }
}

foreach (int number in result)
{
    Console.WriteLine(number);
}
```

الطريقة دي كويسة، لكن لاحظ إننا استخدمنا **foreach** مرتين، مرة علشان نجيب الأرقام اللي أكبر من 5، ومرة علشان نطبعهم. ده يعتبر ممل شوية في الأكواد الكبيرة.

#### الطريقة باستخدام LINQ:
```cs
List<int> numbers = new List<int> { 1, 2, 3, 6, 7, 8, 10 };

var result = from number in numbers
             where number > 5
             select number;

foreach (int number in result)
{
    Console.WriteLine(number);
}
```

زي ما هو واضح في الكود ده، باستخدام **LINQ**، قدرنا نكتب سطرين بس علشان نجيب الأرقام اللي أكبر من 5 ونعرضهم، وده بيوفر علينا وقت وجهد.

- لازم يبدأ بـ from 
- لازم يبقا موجود **range variable** اللي هو number 

### Deferred Execution

الـ **LINQ** بتتميز بحاجة مهمة اسمها **Deferred Execution** تنفيذ مؤجل، وده معناه إن الكود اللي بنكتبه باستخدام **LINQ** ما بيتنفذش فعليًا **غير لما نطلب النتيجة**. 
زي مثلاً لما نستخدم **foreach** لعرض البيانات، ساعتها بس **LINQ** بتبدأ تنفذ الاستعلام.
مبتتنفذش غير لما تعمل عليها Iteration.
يعني result اللي فوق دا بيبقا شايل الـ Query مش نتيجة الـ Query

![[Pasted image 20241014101417.png]]
### Immediate Execution

ممكن تكون في مواقف محتاج فيها إنك تنفذ الاستعلام فورًا بدل ما تنتظر، وهنا بنستخدم حاجة اسمها **Immediate Execution**، وده بيحصل لما تستخدم ميثود زي `ToList()` أو `ToArray()`. مثال:
```cs
var result = (from number in numbers
              where number > 5
              select number).ToList();
```

بكده بنكون نفذنا الاستعلام فورًا وخدنا نسخة من البيانات بالوضع الحالي.
يعني على عكس اللي فوق الـ result هيشيل الـ List نفسها مش الـ Query.


### Method Syntax

في **LINQ**، تقدر تكتب نفس الاستعلام بطرق مختلفة، زي الطريقة اللي فوق (query syntax)، أو باستخدام **Lambda Expressions** واللي بتستخدم شكل الـ **method syntax**، مثال:
هنستخدم [[Cs Extension Methods]] اسمها Where 
وأي Class بيعمل Implement للـ `IEnumerable` هتلاقي الـ LINQ شغال معاها عادي

```cs
var result = numbers.Where(x => x > 5).ToList();
```

الطريقة دي بتكون أكثر شيوعًا، وكتير من المطورين بيفضلوها لأنها بتدي مرونة أكبر وتكون أقرب في الشكل للكود المعتاد.

### الخلاصة

الـ**LINQ** بتمكنك من كتابة استعلامات معقدة على الـ **Collections** في كودك بطريقة بسيطة وسهلة، وبتوفر عليك كتابة كتير جدًا من الكود. 
سواء كنت بتستخدم **query syntax** أو **method syntax**، الاتنين بيقدملك نفس النتيجة، والأفضلية بينهم بتعتمد على ذوقك الشخصي.

### كود للتجربة:
```cs
List<int> numbers = new List<int> { 1, 2, 3, 6, 7, 8, 10 };

// باستخدام LINQ
var result = from number in numbers
             where number > 5
             select number;

foreach (int number in result)
{
    Console.WriteLine(number);
}

// باستخدام Lambda Expressions
var lambdaResult = numbers.Where(x => x > 5).ToList();

foreach (int number in lambdaResult)
{
    Console.WriteLine(number);
}
```

الـ**LINQ** أداة قوية جدًا، وهتلاقي نفسك بتستخدمها كتير في مشاريعك مع التعامل مع البيانات.