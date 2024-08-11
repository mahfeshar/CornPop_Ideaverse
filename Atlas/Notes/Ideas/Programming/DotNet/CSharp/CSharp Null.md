---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-13
---

## Nullable Types
- هي عبارة عن value types بتسمح بال `null`
- بنستخدمها كتير مع ال [[CSharp Input#Get User Input|ReadLine]] لان ممكن ال user ميدخلش قيمة والمفروض تتخزن Null
- يعني مثلا ال`int` مش بيسمح انك تحط `null` كقيمة

```cs
int x = 50;
// x = null; // ERROR

int? Y; //Nullable int, IL (Nullable<int>)
Y = 5000;
Y = null;
```
كل value type ليها ال nullable type بتاعها وال reference types كدا كدا بتسمح بال null
### Casting
طبعًا اتعلمنا ازاي نعمل [[CSharp Type Casting]] وايه النوعين اللي عندي والفرق بينهم، فتعالو نطبق هنا
لو عايز أعملها casting ايه المسموح وايه اللي لا
```cs
int x = 50;
int? Y; //Nullable int
Y = null;

Y = X; // Safe Casting, Implicit
X = Y; // UnSafe, Explicit
X = (int) Y;
```

## Default
لو مش عارف ادي initial value ايه بدي لل data type كلمة `default`
```cs
double D = default;
int [] Arr = default; // null, default value for all reference types
```
## NullReferenceExeption
من أصعب المشاكل اللي ممكن تقابل أي programer هي ال `NullReferenceExeption`  اني بحاول أوصل لحاجة بتشاور على null
```cs
int [] Arr = default; // null
for (int i = 0; i < Arr.Length; i++)
	Console.WriteLine(Arr[i]);
```

فعشان كدا لازم تعمل check عشان توصل لمرحلة ال [[CSharp Protective code]]
```cs
for (int i = 0; (Arr != null) && (i < Arr.Length); i++);
```
### الفرق بين && , &
&&: بيشوف الأول لو محققش المطلوب بيقفل البرنامج يعني فوق لقى الأول بnull فمش هيكمل التاني
&: دي عبارة عن bitwise ولازم يشوف قيمة الاتنين ويعملهم `anding` مع بعض
## Null Propagation (Conditional) Operator
متعملش call لل length لو ال arr ب null
```cs
for (int i = 0; i < Arr?.Length; i++);
```
ممكن أستخدمها أكتر من مرة ورا بعض عادي عشان كدا اسمها Propagation
```cs
class Dept
{
	public string Name;
}

class Employee
{
	public Dept Dept;
}

Empolyee E = default;
Console.WritLine(E.Dept.Name); // Unsafe
Console.WriteLine(E?.Dept?.Name??"Not Available");
```

مثال آخر
```cs
int R = Arr.Length; //Unsafe
int? RR = Arr?.Length; //Safe, Nullable int 
//Arr?.Length === (Arr != null)? Arr.Length : null
int RRR = Arr?.Length??0; //Safe
```