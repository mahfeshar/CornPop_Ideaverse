---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-12
---
- طريقة بستعملها عشان أمدد بيها الأنواع اللي عندي (أزود Method مش موجودة جواها)
	- نوع:  [[Cs Data Types]], [[Cs Class]], [[Cs Struct]], [[Cs Interface]], Data Structure

```cs
int percentage =int.Parse(Console.ReadLine());
if (percentage >= 0 && percentage <= 100)
    Console.WriteLine("Valid percentage");
else
    Console.WriteLine("Invalid percentage");
```
- عايزين حوار الـ Valid دا عشان هيتكرر كتير نعمله Function فزمان كان بيتعمل زي Number Helper وفيه بيتحط فيه كل الـ Methods دي وكان بيبقا [[Cs Static]] سواء الـ Class أو الـ Method
```cs
static class NumberHelper
{
    public static bool IsNumberBetweenRange(int percentage, int min, int max)
    {
        return percentage >=min && percentage <= max;
    }
}
// MAIN
int percentage =int.Parse(Console.ReadLine());
if (NumberHelper.IsNumberBetweenRange(percentage, 0, 100))
    Console.WriteLine("Valid percentage");
else
    Console.WriteLine("Invalid percentage");
// بنستخدمها عن طريق الكلاس
```
- بس الطريقة الأصح إني أستخدم الـ Extension methods وهي سهلة الإستخدام عن طريق كلمة `this`

![[Pasted image 20241012091519.png]]
- تعتبر بتبقا موجودة خلاص جوا الـ int وأقدر أستخدمها مع أي object من نوع الكلاس اللي عملتهاله
```cs
static class NumberHelper
{
    public static bool IsNumberBetweenRange(this int percentage, int min, int max)
    {
        return percentage >=min && percentage <= max;
    }
}
// IsNumberBetweenRange(int percentage, this int min // ERROR

// MAIN
int percentage =int.Parse(Console.ReadLine());
if (percentage.IsNumberBetweenRange(0, 100))
    Console.WriteLine("Valid percentage");
else
    Console.WriteLine("Invalid percentage");
// Also we can use it in default way (WITH CLASS)
if (NumberHelper.IsNumberBetweenRange(percentage, 0, 100))
    Console.WriteLine("Valid percentage");
else
    Console.WriteLine("Invalid percentage");
```
- اللي بييجي بعد `this` هو دا الـ Class اللي بعمله الـ Method
- زي مانت خدت بالك لازم الـ Class والـ Method يبقوا [[Cs Static]]
- جرت العادة إن الإسم بيبقا فيه Helper أو Extension 
- مينفعش أنقل this لأي حتة بعد الـ Parameter الأول
- لو عندي instance method وعملت بنفس الإسم extension method فالـ extension بيبقا أولويتها أقل فهياخد الـ instance
- تقدر تخليها ترجع value أو متعملش return ودي حاجة ترجعلك انت ولكن الأحسن إنك ترجع value من نفس النوع اللي هتغير عليه عشان تمكنك من الـ Method chaining
  وكمان الـ value types لو غيرت فيها فمش هتفرق فدي مشكلة [[Cs Pass parameters#Pass Value Type|Pass Value Types]]

## Example
```cs

```