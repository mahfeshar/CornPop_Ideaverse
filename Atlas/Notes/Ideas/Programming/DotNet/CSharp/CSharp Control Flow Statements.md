---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-06
---

![[Control Flow Statments.png]]
# Selection Statements
## If Else

```csharp
if (condition1)
{
  // block of code to be executed if condition1 is True
} 
else if (condition2) 
{
  // block of code to be executed if the condition1 is false and condition2 is True
} 
else
{
  // block of code to be executed if the condition1 is false and condition2 is False
}
```
#### example:
```csharp
int time = 22;
if (time < 10) 
{
  Console.WriteLine("Good morning.");
} 
else if (time < 20) 
{
  Console.WriteLine("Good day.");
} 
else 
{
  Console.WriteLine("Good evening.");
}
// Outputs "Good evening."
```
### Short Hand If .. Else (Ternary Operator)
- بستخدمها عشان أحط قيمة في variable على حسب شرط معين
- بتحتاجها دايمًا لما تيجي تعمل Select من Database
```csharp
variable = (condition) ? expressionTrue :  expressionFalse;

variable = (condition) ? expressionTrue: (Else if Condition)? expressionTrue: expressionFalse;
```
#### example:

```csharp
int time = 20;
if (time < 18) 
{
  Console.WriteLine("Good day.");
} 
else 
{
  Console.WriteLine("Good evening.");
}

//******************************//

int time = 20;
string result = (time < 18) ? "Good day." : "Good evening.";
Console.WriteLine(result);
```
## Switch
- بتختار حاجة من ال blocks الكتير اللي عندك وبتنفذها لو الشرط اتحقق
- ال break هنا mandatory ولازم تبقا موجودة
#### example 1
```csharp
int day = 4;
switch (day) 
{
  case 1:
    Console.WriteLine("Monday");
    break;
  case 2:
    Console.WriteLine("Tuesday");
    break;
  case 3:
    Console.WriteLine("Wednesday");
    break;
  default:
	Console.WriteLine("def");
	break;
}
// Outputs "Thursday" (day 4)
```
#### example 2: With when
```cs
double degree = double.Parse(Console.ReadLine());

switch (degree)
{
    case double d when (d >= 0 && d <= 50):
        Console.WriteLine("F");
        break;
    case double d when (d >= 51 && d <= 65):
        Console.WriteLine("D");
        break;
    case double d when (d >= 66 && d <= 75):
        Console.WriteLine("C");
        break;
    case double d when (d >= 76 && d <= 85):
        Console.WriteLine("B");
        break;
    case double d when (d >= 86 && d <= 100):
        Console.WriteLine("A");
        break;
    default:
        Console.WriteLine("Null");
        break;
}
```

#### example 3: Same body

- لو ال body بتاع اتنين case هيبقا واحد فممكن مكررش وأعملهم group

```cs
int x = 2;
switch (x)
{
	case 1:
	case 3:
		Console.WriteLine("Odd");
		break;
	case 2:
	case 4:
		Console.WriteLine("Even");
		break;
	default:
		Console.WriteLine("Out of Range");
}
```

### Fall-through
- انه بكل بساطة ممكن أخد ال body من أول case ومن التاني ومن التالت وهكذا
- وفي الطريقة دي بستخدم معاها ال `goto`
```cs
int Value = 3000;

switch (Value)
{
	case 3000:
		Console.WriteLine("Option 03");
		Console.WriteLine("Option 02");
		Console.WriteLine("Option 01");
		break;
	case 2000:
		Console.WriteLine("Option 02");
		Console.WriteLine("Option 01");
		break;

	case 1000:
		Console.WriteLine("Option 01");
		break;
	default:
		Console.WriteLine("NA");
		break;
}

switch (Value)
{
	case 3000:
		Console.WriteLine("Option 03");
		//Console.WriteLine("Option 02");
		//Console.WriteLine("Option 01");
		goto case 2000;
	//break;
	case 2000:
		Console.WriteLine("Option 02");
		//Console.WriteLine("Option 01");
		goto case 1000;
	//break;
	case 1000:
		Console.WriteLine("Option 01");
		break;
	default:
		Console.WriteLine("NA");
		break;
}
```

> انك تستخدم ال `goto` عموما مش أحسن حاجة ودي الحالة الوحيدة اللي ممكن تستخدمها فيها وحتى استخدامها على مسئوليتك
### Switch vs If Else
- لو فيه checks كتير استخدمها ومتستخدمش If Else لان ال If Else بتاخد Time Complexity = O(N)
  انما ال Switch بتاخد O(1) لأنها بتستخدم Hash table 
  فبالنسبالها كلمة case عبارة عن label او يفطة وهي بتعمل jump عليها
- اقدر استخدمها برضو مع ال strings بس في الحالة دي انسى كل الكلام اللي فوق بتاع الفرق بينها وبين ال If Else لأنها هتاخد نفس ال time complexity 
  ودا بسبب انها مش بتستخدم ال jump table اللي قولنا عليه 
- لما بستخدم string أكنه بيحول ال code ل If Else
- فلو عدد ال options صغير شوية مش هتفرق تستخدم ايه انما لو عدد ال cases أكبر شوية فاستخدم ال switch لانه في الحالة دي بيستخدم ال Hash table
# Iteration Statements
We should have:
1. initial value
2. condition
3. counter + , -
## For

```cs
// for (initial value; condition; counter)
for (int i = 0; i < 5; i++)
{
	Console.WriteLine(i);
}
```
### Nested Loops
اننا نحط loop جوا loop

```csharp
// Outer loop
for (int i = 1; i <= 2; ++i) 
{
  Console.WriteLine("Outer: " + i);  // Executes 2 times

  // Inner loop
  for (int j = 1; j <= 3; j++) 
  {
    Console.WriteLine(" Inner: " + j); // Executes 6 times (2 * 3)
  }
}
```
## Foreach
We use it a lot with [[CSharp Arrays]]
```csharp
string[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
foreach (string i in cars) 
{
  Console.WriteLine(i);
}
```
## While
طول ما الشرط true اللي جواها هيتنفذ
```csharp
int i = 0;
while (i < 5) 
{
  Console.WriteLine(i);
  i++;
}
// 0 1 2 3 4
```

>[!warning] Do not forget to increase the variable used in the condition, otherwise the loop will never end!

## Do/While
زي while بالظبط بس هو هينفذ الأول وبعدين يعمل check على الشرط
```csharp
int i = 0;
do 
{
  Console.WriteLine(i);
  i++;
}
while (i < 5);
// 0 1 2 3 4
```


