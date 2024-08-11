---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-04
---
- هي لغة [[Strongly and weakly typed languages#Strongly Typed|Strongly Typed]]: يعني وأنت بتعرف أي قيمة لازم تحدد نوع الdata اللي هتخزنها 
## Primitive types table (Built-in)
- [[CSharp Value and Reference Types#Value Types|Value Type]]
- بتتخزن في حتة في الميموري اسمها Stack بطريقة ال Value
- اللي بتبقا جاهزة وجاية مع اللغة

![[Pasted image 20240312124448.png]]

```cs
// Integer
// byte, int, short, long
byte x = 20; // 0 : 255
Console.WriteLine(byte.MinValue + " " + byte.MaxValue);
Console.WriteLine(sizeof(byte)); // In memory : Space (1 byte)

// Real (Fraction)
// decimal, float, double
double x = 2.5; // default type for fraction
float y = 5.6f;
decimal z = 4.1m;

// One character
char x = '+'; // Single quote

// Text
string x = "Mahmoud"; // Double quote
string path = @"c:\Users\Mahmoud"; // @ for skip the skip char

// Boolean
bool b = true;
bool x = false; // 0 or 1 not allowed


// Non Primitive //

// Time
// DateTime
```
### .NET types 
- عندي types زي ما واضح في الصورة فوق لل  .NET عشان نفس حوار إنها تبقا cross lang
- مش أحسن حاجة إنك تستخدمها واستخدم نظريتها في ال C# أحسن
### unsigned types
- لو عايز ال variable يخزن قيم من غير إشارة (ميخزنش السالب) فعندنا data types جاهزة للحوار دا
- اكتب u قبل ال data type ومش موجود لكله

```cs
uint x = -2; // ERROR
```
### _ : Discards
- ممكن نستخدمها عشان نخلي الرقم مقروء أكتر اني افصل بين كل 3 أرقام مثلًا

```cs
int X = 1_000_000_000;
X = 0x_00_00_FA_12; //Hex
byte y = 0b_0101_1100; //Binary
```
### fraction
العلامة العشرية بكل بساطة بتبقا *double*، فلو عايز أخزنها في float او  decimal لازم اعرف الكومبايلر
```cs
double x = 15.3;
float y = 15.3F;
decimal z = 13.5M;
```

## Non Primitive Data Types (User Define)
- [[CSharp Value and Reference Types#Reference Types|Reference Types]]
- بتتخزن في حتة في الميموري اسمها **Heap** بطريقة ال Reference
- اللي بعملها بنفسي
- زي ال [[CSharp Class]], [[CSharp Struct]], [[CSharp Arrays]], [[CSharp Enums]]
### Classes
```cs
public class Vehicle
{
	public int Id;
	public short Year;
	public string Make;

	public void DriveVehicleForward()
	{
		// bla bla bla
	}
}
```

## Numeric Formatting
![[Pasted image 20240312131437.png]]

```cs
Console.WriteLine($"Equation : {X,5}+{Y,-5}={X + Y:X}");
```
الخمسة اللي حطيتها مع ال x دي يعني هيطبع في 5 digit ولو خليتها بالسالب هيظهر الرقم عالشمال مش عاليمين
ممكن نحول من data type لنوع تاني من خلال [[CSharp Type Casting]]
