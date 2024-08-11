---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-06
---
عندنا نوعين من ال Casting:
- **Implicit Casting** (automatically) - converting a smaller type to a larger type size  
    `char` -> `int` -> `long` -> `float` -> `double`  
- **Explicit Casting** (manually) - converting a larger type to a smaller size type  
    `double` -> `float` -> `long` -> `int` -> `char`

## Implicit Casting
- No need of Casting
```cs
int myInt = 9;
double myDouble = myInt //Automatic casting: int to double
//Safe Casting , No RunTime Errors 
```
## Explicit Casting
### Memory
- بيحصل مع ال unsafe casting، ان ممكن ال data type يشيل القيمة اللي هديهاله وممكن لا
- يعني أحاول أحط حاجة كبيرة في حاجة صغيرة في ال memory فمش هيقبل
```cs
int x = 5;
double y = 50;

x = (int) y;

Y = long.MaxValue;
x = (int) y; 
// overflow, but no error here, just garbage value
```
- في حالة اني اديتله قيمة متقدرش تشيله 
  في الحالة دي ال CLR مش بيرمي exception ويوقف البرنامج وفي الحالة دي ال exception unhandled وبيفضل كدا لحد اما بعمله [[CSharp Handle Exception]]
- بيملى الميموري وبعدين لو خلصت وعايز أكمل برمي اللي فيها وأبدأ أملى تاني
```cs
int x = 300;
byte y = (byte) x; // byte -> 255
// 300 = 255 + 44
```
#### Checked
- بيطلع Exception لو حصل Overflow في الحاجة اللي بخزن فيها
- وفي المستقبل لو عايز تعمل handling عادي
```cs
int x = 300;
checked 
{
	byte y = (byte) x; // Unhandled exception. System.OverflowException
}
```
#### Unchecked
- كل فايدتها ان لو حصل overflow ميرميش exception ومش بيتم استخدامها غير مع الoverflow errors
- بستخدمها جوا ال checked بلوك لو فيه جزء جواه مش عايز يتعمله check 
### Data Type
#### C# Method (Parse)
- لو عايز أغير من نوع للتاني وهو مش سامح بكدا بستخدم `Parse`
```cs
int a = Console.ReadLine(); // String -> int : ERROR

int a = int.Parse(Console.ReadLine());
// All data types have that exept Strings

// ERROR
int x = 5;
string y = string.Parse(x);
```

#### .NET Method (Convert)
ممكن نغير من نوع لنوع تاني باستخدام شوية methods كدا 
`Convert.ToBoolean`, `Convert.ToDouble`, `Convert.ToString`, `Convert.ToInt32` (`int`) and `Convert.ToInt64` (`long`)
```cs
int myInt = 10;
double myDouble = 5.25;
bool myBool = true;

Console.WriteLine(Convert.ToString(myInt));    // convert int to string
Console.WriteLine(Convert.ToDouble(myInt));    // convert int to double
Console.WriteLine(Convert.ToInt32(myDouble));  // convert double to int
Console.WriteLine(Convert.ToString(myBool));   // convert bool to string
```

> [!info]
> بالنسبة لل Convert ففيها ميزة قوية جدًا وهي إن لو بتعمل convert ل int مثلًا والقيمة null فهو هيحطها ب zero 
> هيهندل الدنيا لوحده

