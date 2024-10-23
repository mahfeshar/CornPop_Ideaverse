---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-23
---

الـ `is` في C# هو **مشغل شرطي** يستخدم للتحقق مما إذا كان كائن معين من نوع محدد. يقوم هذا المشغل بإرجاع قيمة **true** إذا كان الكائن المتحقق منه يتطابق مع النوع المحدد، و **false** إذا لم يكن كذلك.

---
العملية هترجع True في 3 حالات:
- لو هو object من نفس النوع أو من نفس الكلاس
- لو هو object من كلاس بيورث من الكلاس الأساسي
- لو هو بيساوي `null`
### الصيغة الأساسية:
```csharp
if (object is Type)
{
    // Code to execute if object is of the specified type
}
```

### مثال بسيط:
```csharp
object myObject = "Hello, World!";

if (myObject is string)
{
    Console.WriteLine("The object is a string.");
}
else
{
    Console.WriteLine("The object is not a string.");
}
```

#### شرح المثال:
- هنا لدينا كائن `myObject` يحمل قيمة نصية ("Hello, World!").
- نستخدم العبارة الشرطية `myObject is string` للتحقق مما إذا كان الكائن من النوع `string`.
- بما أن الكائن هو بالفعل سلسلة نصية، سيتم طباعة `"The object is a string."`.

### استخدام الـ `is` مع النمط (Pattern Matching):

في الإصدارات الأحدث من C# (بدءًا من C# 7.0)، يمكن استخدام الـ `is` مع النمط لتفادي القيام بعملية التحويل (casting) يدويًا:

```csharp
// Before
object myObject = "Hello, World!";

if (myObject is string)
{
	string str = (string) myObject; // Casting
}


// After
object myObject = "Hello, World!";

if (myObject is string myString)
{
    Console.WriteLine($"The object is a string: {myString}");
}
```

#### شرح هذا المثال:
- هنا نتحقق من نوع الكائن، وإذا كان من النوع `string`، نقوم بتعريف متغير جديد `myString` ليحمل القيمة.
- هذه الطريقة أكثر كفاءة لأنها تتحقق وتحول النوع في نفس الخطوة.

### الاستخدامات:
- التحقق من الأنواع (type checking) أثناء وقت التشغيل (runtime).
- مفيد عند التعامل مع الأنواع العامة أو الأنواع الموروثة (inheritance).

هل تحتاج إلى مزيد من الأمثلة أو توضيح حول كيفية استخدامه في سيناريوهات معينة؟