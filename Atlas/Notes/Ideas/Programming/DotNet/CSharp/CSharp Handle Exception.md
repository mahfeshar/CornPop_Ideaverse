---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-07
---
- تبقا عامل حسابك على الغلطات لما تحصل ترد عليها بالبرنامج بتاعك
- بيبقا معاها حاجة اسمها Log Exception: هي انك تحتفظ بتفاصيل المشكلة عشان تشوفها بعدين وتعرف حصلت إزاي وكدا
### إزاي أعمل Log:
- ممكن أحتفظ بالماسدج جوا Data Base مثلًا وأعملها Table مخصوص
- ممكن أحتفظ في Files على السيرفر وفيه Tools ممكن تستخدمها زي SeriLog, NLog
- ممكن نستخدم Event Viewer بتاع ال Windows
بيطلع حاجة اسمها Auditing: بتحاول تعرف سيناريو معين حصل لليوزر ^707d90
### ازاي أعمل Handling
1. الStatic Message: بيطلع رسالة ايرور لكل المشاكل اللي بتقابل المستخدم وبتبقا نفسها لكله
2. ال Friendly Message: اني أعرفه إيه اللي حصل بالظبط وأفهمه الدنيا
3. ال Friendly Message + Recommended Fix: دي أحسن من اللي فاتوا اني بقوله ازاي يحلها كمان (**الأكثر إستخدامًا**)
4. ال Friendly Message + Recommended Fix + Try to fix: بعرفه كل حاجة وكمان بحاول أنا أحلهاله ودي أفضل واحدة بس مش الأكتر استخدامًا
# Handling
## Exception Class
- عبارة عن كلاس جاهز عشان أحدد ال Exception اللي ممكن يحصل
- بعرف منه variable عشان أقدر أستخدمه

```cs
Exception ex;
ex.Message; // The message of the error
```
جواه فيه كل أنواع ال Exceptions اللي تقدر تستخدمها والمشهورة
## Try … Catch
- بتحط الكود بتاعك اللي ممكن يحصل فيه مشكلة في Try (بيتعمله Test)
- لو حصل مشكلة بيروح على جزء ال catch
- بنعمل في الCatch خطوتين (Handle - Log)
- الكود مش بيقف بعدها عادي (ودي الميزة)
- مش Validation دي عبارة عن حل  للمشاكل اللي ممكن تقابل ال User
- ممكن تستخدم أكتر من Catch لنفس ال Try

```cs
try 
{
  //  Block of code to try
}
catch (Exception ex) // You can use it withoud ()
{
  //  Block of code to handle errors
}
```

#### Example

```cs
try
{
    var x1 = int.Parse(Console.ReadLine());
    var x2 = int.Parse(Console.ReadLine());

    Console.WriteLine(x1 / x2);
}
catch // OR : catch (Exception ex)
{
    Console.WriteLine("Error"); // OR: ex.Message
}


// ------ //
// Bad use
try
{
    var x1 = int.Parse(Console.ReadLine());
    var x2 = int.Parse(Console.ReadLine());

    Console.WriteLine(x1 / x2);
}
catch (OverflowException)
{
    Console.WriteLine("OverFlow");
}
catch (DivideByZeroException)
{
    Console.WriteLine("Divide by zero");
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}


// -----------------
// Best one
// Throw Every Exception with your own message
throw OverflowException("My Message");
throw DivideByZeroException("My Message");
```
## Finally
- بيبقا بعد ال Catch
- وبيتنفذ اللي جواه في أي حالة سواء فيه مشكلة أو مفيش مشاكل خالص
- ممكن تحتاجة يقفل ال Connection مع ال DB فيقفله في الحالتين
- مثلًا تخليه يمسحلك ال Garbage Collector
- We talked about it at [[CSharp Value and Reference Types#Garbage Collector|Garbage Collector]]
- مش شرط تبقا موجودة
## Throw
بستخدمها عشان **أعمل مشكلة** معينة وبستخدم معاها class `Exception`
بعمل Custom Exception

```cs
string name = Console.ReadLine();

if (name == "") // If empty
{
    throw new Exception("Name can not be empty, please insert valid name"); 
    // I used the third handling form (Friendly + Recommended Fix)
}
```

# Log
- We will use [[CSharp Handle Exception#^707d90|event viewer]] -> Windows Logs -> Application
- الطريقة دي مش Recommended أو كدا
- عشان تعمل كدا لازم تحدد إنك شغال على VS as administrator 
- بتعامل معاه من خلال باكدج جاهزة اسمها Diagnostics (لو مش موجودة بنعملها Install)
- بستخدم منها class اسمه `EventLog`
```cs
using System.Diagnostics;

EventLog log = new EventLog(); // New for heap (new object from this class)
log.Source = "Hr System";
log.WriteEntry(ex.Message, EventLogEntryType.Error) // Message , Type
// You can add more

```

![[Pasted image 20240707172040.png]]
```cs
try
{
    var x1 = int.Parse(Console.ReadLine());
    var x2 = int.Parse(Console.ReadLine());

    Console.WriteLine(x1 / x2);
}

catch (Exception ex)
{
    Console.WriteLine(ex.Message);
    EventLog log = new EventLog();
    log.Source = "Corn Pop";
    log.WriteEntry(ex.Message, EventLogEntryType.Error);
}
```