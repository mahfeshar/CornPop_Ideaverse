---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-14
---
هنركز على ثلاث مواضيع رئيسية: 

1. **Quantifiers**.
2. **Partitioning** أو تقسيم البيانات.
3. **Set Operations** أو العمليات على المجموعات.

### 1. الكوانتي فايرز (Quantifiers)

الكوانتي فايرز هي عبارة عن **Test Methods**، ودي وظيفتها إنها تختبر إذا كانت **List** أو **Collection** معينة بتتحقق فيها شروط محددة ولا لأ. 
الكوانتي فايرز الأساسية في LINQ هي:

- **All**
- **Any**
- **Contains**

#### 1.1 **All**
الميثود دي بتختبر إذا كانت كل العناصر في الـ List بتتحقق فيها شرط معين.


```cs
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
bool allGreaterThanZero = numbers.All(n => n > 0);
Console.WriteLine(allGreaterThanZero); // True
```

في المثال ده، `All` بتختبر إذا كانت كل الأرقام أكبر من 0، وبما أن ده صحيح، بترجع **True**. لو كان فيه عنصر واحد أقل من 0، كانت هترجع **False**.

#### 1.2 **Any**
الميثود دي بتختبر إذا كان فيه عنصر واحد على الأقل بيحقق الشرط.

```cs
bool hasNegative = numbers.Any(n => n < 0);
Console.WriteLine(hasNegative); // False
```

هنا، بنستخدم `Any` علشان نعرف لو فيه أي رقم أقل من 0. بما إن مفيش أي أرقام سالبة في القائمة، النتيجة بتكون **False**.

وكمان ممكن تستخدم `Any` بدون شرط:

```cs
bool isNotEmpty = numbers.Any();
Console.WriteLine(isNotEmpty); // True
```

النتيجة **True** لأن القائمة مش فاضية. لو كانت فاضية، كانت هترجع **False**.

#### 1.3 **Contains**
الميثود دي بتختبر إذا كانت الـ List بتحتوي على قيمة معينة.

```cs
bool containsFive = numbers.Contains(5);
Console.WriteLine(containsFive); // True
```

هنا، بنختبر إذا كانت الـ List بتحتوي على الرقم 5. بما أن الرقم موجود، بترجع **True**.

### 2. تقسيم البيانات (Partitioning)

في LINQ، تقدر تقسم البيانات باستخدام عمليات زي **Take**، **Skip**، **TakeWhile**، و**SkipWhile**. 
العمليات دي بتساعدك إنك تاخد جزء معين من البيانات أو تتخطى جزء معين منها.

#### 2.1 **Take**
الميثود دي بتاخد عدد معين من العناصر من البداية.

```cs
var firstThree = numbers.Take(3);
foreach (var num in firstThree)
{
    Console.WriteLine(num); // 1, 2, 3
}
```

في المثال ده، `Take` بتاخد أول 3 عناصر من القائمة.

#### 2.2 **Skip**
الميثود دي بتتخطى عدد معين من العناصر من البداية.

```cs
var skipTwo = numbers.Skip(2);
foreach (var num in skipTwo)
{
    Console.WriteLine(num); // 3, 4, 5
}

var skipTake = numbers.Skip(6).Take(4); 
// You can skip then take
```

هنا، `Skip` بتتخطى أول عنصرين وترجع الباقي.

#### 2.3 **`TakeWhile`**
الميثود دي بتاخد العناصر طالما الشرط محقق. أول ما الشرط يتوقف، بتتوقف عن أخذ المزيد من العناصر.

```cs
var takeWhileLessThanFour = numbers.TakeWhile(n => n < 4);
foreach (var num in takeWhileLessThanFour)
{
    Console.WriteLine(num); // 1, 2, 3
}
```

#### 2.4 **SkipWhile**
الميثود دي بتتخطى العناصر طالما الشرط محقق، وأول ما الشرط يتوقف، بتبدأ ترجع باقي العناصر.

```cs
var skipWhileLessThanThree = numbers.SkipWhile(n => n < 3);
foreach (var num in skipWhileLessThanThree)
{
    Console.WriteLine(num); // 3, 4, 5
}
```

#### 2.5 **Chunk**

بتقسم لك الـ **List** أو الـ **Collection** إلى أجزاء صغيرة أو "مجموعات" بناءً على الحجم اللي إنت بتحدده. 
يعني لو عندك **List** كبيرة، تقدر باستخدام **Chunk** تقسمها إلى مجموعات أصغر، وكل مجموعة فيها عدد معين من العناصر حسب الحجم اللي إنت محدده.

لو عندك قائمة طويلة من الأرقام، وعايز تقسمهم إلى مجموعات، وكل مجموعة تحتوي على 3 أرقام:

```cs
var numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

var chunks = numbers.Chunk(3);

foreach (var chunk in chunks)
{
    Console.WriteLine("New Chunk:");
    foreach (var num in chunk)
    {
        Console.WriteLine(num);
    }
}
```

في المثال ده، الميثود **Chunk(3)** بتاخد كل 3 عناصر من **numbers** وتعمل منهم "مجموعة" أو **Chunk**. يعني هتقسم القائمة دي إلى ثلاث مجموعات:
- المجموعة الأولى: { 1, 2, 3 }
- المجموعة الثانية: { 4, 5, 6 }
- المجموعة الثالثة: { 7, 8, 9 }

بعد كده بنستخدم **foreach** علشان نلف على كل **Chunk** أو مجموعة، وبنطبع العناصر اللي فيها.

```
New Chunk:
1
2
3
New Chunk:
4
5
6
New Chunk:
7
8
9
```

### فائدة الميثود **Chunk**:

الميثود دي مفيدة جداً لما تكون بتتعامل مع قوائم كبيرة وعايز تقسمها لأجزاء صغيرة علشان تسهّل معالجتها. زي مثلاً لو عندك قائمة كبيرة من البيانات وعايز تعالج كل مجموعة بيانات مع بعضها في نفس الوقت باستخدام عمليات متعددة أو معالجات متوازية.

**Chunk** بتوفر لك طريقة سهلة لتقسيم البيانات إلى مجموعات من نفس الحجم وتتعامل معاها بطريقة منظمة بدون تعقيد.
### 3. عمليات المجموعة (Set Operations)

عمليات المجموعة في LINQ بتسمح لك إنك تتعامل مع مجموعات البيانات بطريقة منظمة زي إنك تشيل التكرارات، تجيب التقاطعات، أو حتى توحد القائمتين.

#### 3.1 **Distinct**
الميثود دي بتشيل التكرارات من القائمة.

#### مثال:

```cs
List<int> numbersWithDuplicates = new List<int> { 1, 2, 3, 3, 4, 4, 5 };
var distinctNumbers = numbersWithDuplicates.Distinct();
foreach (var num in distinctNumbers)
{
    Console.WriteLine(num); // 1, 2, 3, 4, 5
}
```

#### 3.2 **Except**
الميثود دي بتجيب كل العناصر الموجودة في القائمة الأولى اللي مش موجودة في القائمة التانية.

#### مثال:

```cs
List<int> otherNumbers = new List<int> { 3, 4 };
var exceptNumbers = numbers.Except(otherNumbers);
foreach (var num in exceptNumbers)
{
    Console.WriteLine(num); // 1, 2, 5
}
```

#### 3.3 **Intersect**
الميثود دي بتجيب العناصر المشتركة بين القائمتين.

#### مثال:

```cs
var intersectNumbers = numbers.Intersect(otherNumbers);
foreach (var num in intersectNumbers)
{
    Console.WriteLine(num); // 3, 4
}
```

#### 3.4 **Union**
الميثود دي بتوحد القائمتين مع بعض، مع إزالة التكرارات.

#### مثال:

```cs
var unionNumbers = numbers.Union(otherNumbers);
foreach (var num in unionNumbers)
{
    Console.WriteLine(num); // 1, 2, 3, 4, 5
}
```

### 4. **OfType** و **Where(x => x is Type)**
الفرق بين `OfType` و `Where` مع `is` بسيط ولكن مهم:

- **OfType** بترجع فقط العناصر اللي من النوع اللي تحدده. بتتجاهل باقي الأنواع بدون ما تحتاج تتحقق منهم.
- **Where مع is** بتديك المرونة إنك تتحقق من النوع وتطبق شرط تاني في نفس الوقت.

#### مثال:

```cs
List<object> mixedList = new List<object> { "string", 1, 2, "another string", 3 };
var stringsOnly = mixedList.OfType<string>(); // بترجع العناصر اللي نوعها string
var numbersOnly = mixedList.Where(x => x is int); // بترجع العناصر اللي نوعها int
```

في المثال ده، `OfType<string>` بترجع السلاسل النصية فقط، بينما `Where` مع `is` بترجع الأرقام فقط.

### **الخلاصة**

- **Quantifiers** بتساعدك تعمل اختبار للـ List زي `All`, `Any`, و `Contains`.
- **Partitioning** بيساعدك تاخد جزء معين أو تتخطى جزء معين من البيانات باستخدام `Take`, `Skip`, `TakeWhile`, و `SkipWhile`.
- **Set Operations** زي `Distinct`, `Except`, `Intersect`, و `Union` بتساعدك تتعامل مع المجموعات بطريقة منظمة.
- **OfType** بترجع العناصر اللي من النوع اللي تحدده فقط، أما **Where مع is** فبتديك مرونة أكبر في التحقق من النوع.

LINQ بتبسط التعامل مع البيانات بشكل كبير وبتخليك تكتب كود أقصر وأوضح. جرب الأمثلة دي بنفسك وشوف قد إيه ممكن تسهل شغلك!
