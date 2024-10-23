---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-23
---
بيختلف عن الـ [[Cs Type Casting]]
الـ `as` في C# هو (Casting Operator) يستخدم لتحويل كائن إلى نوع معين **بشكل آمن**. 
**إذا لم يكن الكائن من النوع المطلوب، فإنه يُرجع *null* بدلاً من التسبب في استثناء (Exception).** 
هذا يجعل استخدامه أكثر أمانًا مقارنةً باستخدام التحويل التقليدي (`(Type)`) الذي قد يسبب استثناءً إذا فشل التحويل.

### الصيغة الأساسية:
```csharp
object myObject = ...;
Type myVariable = myObject as Type;
```

- إذا كان `myObject` يمكن تحويله إلى النوع `Type`، فسيتم التحويل وتخزينه في المتغير `myVariable`.
- إذا لم يكن من الممكن التحويل، فإن `myVariable` سيأخذ قيمة `null`.

### مثال بسيط:
```csharp
object myObject = "Hello, World!";
string myString = myObject as string;

if (myString != null)
{
    Console.WriteLine($"The string is: {myString}");
}
else
{
    Console.WriteLine("The object is not a string.");
}
```

### شرح المثال:
- هنا لدينا كائن `myObject` من النوع `object` ويحمل سلسلة نصية.
- نستخدم `as` لتحويل هذا الكائن إلى `string`. إذا كان الكائن بالفعل سلسلة نصية، سيتم تخزينه في المتغير `myString`.
- إذا لم يكن التحويل ممكنًا (على سبيل المثال، إذا كان `myObject` يحمل نوعًا آخر مثل `int`)، سيأخذ `myString` قيمة `null`.
- نتحقق بعد ذلك من قيمة `myString` للتأكد من نجاح التحويل.

### مثال آخر:
```csharp
object myObject = 123;
string myString = myObject as string;

if (myString == null)
{
    Console.WriteLine("The object is not a string.");
}
```

### في هذا المثال:
- الـ`myObject` يحمل قيمة عدد صحيح `int`.
- عند محاولة تحويله إلى `string` باستخدام `as`، لن يتمكن من التحويل لأن الكائن ليس من النوع `string`.
- وبالتالي، ستكون قيمة `myString` هي `null`، ويتم تنفيذ الكود داخل الجملة الشرطية.

### مميزات استخدام `as`:
1. **آمن**: بدلاً من إطلاق استثناء عند فشل التحويل كما في التحويل التقليدي، يُرجع `null`، مما يسمح بمعالجة الفشل بشكل سلس.
2. **أقل تكلفة**: بدلاً من إجراء عملية فحص النوع مرتين (مرة باستخدام [[Cs is]] ثم التحويل)، يمكنك التحويل مباشرة باستخدام `as`، مما يحسن الأداء في بعض الحالات.

### ملاحظة:
- مشغل `as` يعمل فقط مع **الأنواع المرجعية** (Reference Types) و **الأنواع القابلة للتحويل ضمنيًا** (nullable types). 
- لا يمكن استخدامه مع الأنواع البدائية (مثل `int` أو `bool`).