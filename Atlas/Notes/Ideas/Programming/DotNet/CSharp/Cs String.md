---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-13
---
## Strings
- بنستخدمها عشان نخزن فيها النصوص text
```cs
string greeting = "Hello";
string greeting2 = "Nice to meet you!";
```
- هي عبارة عن [[Cs Value and Reference Types#Reference Types|Reference Type]]
- عبارة عن class وجواه properties and methods
- ال string عبارة عن [[Mutable vs Immutable#Immutable Objects|immutable]] يعني لما بضيف حاجة أو بشيل حاجة بيعمل string جديدة خالص مختلفة عن القديمة ودا بيأثر على سرعة العملية وعلى الميموري
- عبارة عن [[Array#Static Arrays|array]] of characters وطبيعي لازم تبقا معرفها مسبقا هي هتاخد size قد ايه وهنا المشكلة
- الحل هو ال StringBuilder واللي بيفرق عنها في حاجات كتير [[CSharp StringBuilder]]
## Why string always reference type?
- في كل لغات البرمجة اللي قابلتنا عرفنا ان ال string هو reference مش value
  لاني لما باجي أحجز string مش ببقا عارف انا هحجز قد ايه بالظبط في ال memory انما لو جيت تحجز `int x` هو بيبقا عارف انه هيحجز 4 byte 
- ولما أجي اعمل allocate بقا هيعرف انا هحجز كام byte بالظبط 
```cs
string str; //reference
str = "ABC"; // عرف انا هحجز قد ايه
```
مش هحتاج في ال Csharp اني اعمل new لان اللغة نفسها بتظبط الحاجات دي

## String Length
هي عبارة عن **property** بترجع عدد الحروف اللي بيتكون منها
*خد بالك اننا مش بنكتب قوسين فيها*
```cs
string txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
Console.WriteLine(txt.Length); // 26
```
## Other Methods

### Formatting
عندنا methods كتير في ال string بس أشهر اتنين هم `()ToUpper() and ToLower`

```cs
string txt = "Hello World";
Console.WriteLine(txt.ToUpper()); // HELLO WORLD
Console.WriteLine(txt.ToLower()); // hello world
```

`Trim()` : Remove any leading or trailing blank spaces

```cs
string val1 = " a";
string val2 = "a ";
Console.WriteLine(val1.Trim() == val2.Trim()); // True
```

`Contains()`, `StartsWith()` , `EndsWith()`

```cs
string pangram = "The quick brown fox jumps over the lazy dog.";
Console.WriteLine(pangram.Contains("fox")); //True
Console.WriteLine(pangram.Contains("cow")); // False
```
### Searching
`IndexOf('a')`, `LastIndexOf("Hello")`
بيقبلوا characters أو strings

### Substrings
`Substring(startIndex)`, `Substring(startIndex, length)`

### Replacing
`Replace('a', '!')`, `Replace("corn", "popcorn")`

### Null checking
`String.IsNullOrEmpty(str)`, `String.IsNullOrWhiteSpace(str)`

### Splitting
`str.Split(' ')` with delimiter.

### Converting
We can convert from number to string and from string to number by [[Cs Type Casting#Explicit Casting|Explicit Casting]].
Or by `i.ToString(format);`

![[Pasted image 20240715114820.png]]
![[Pasted image 20240715114833.png]]
- حد بالك من حتة ال C0 دي عشان كدا خلى اللي بعد العلامة العشرية 0 رقم ولو عايز أخليه رقم واحد أستخدم C1 وهكذا
## Concatenation
بنستخدم علامة `+` عشان أدمج اتنين سوا
```cs
string firstName = "Pop";
string lastName = "Corn";
string name = firstName + lastName;
Console.WriteLine(name);
```
ممكن نستخدم برضو `string.Concat()` وهي عبارة عن method جوا ال string
```cs
string firstName = "Pop";
string lastName = "Corn";
string name = string.Concat(firstName, lastName);
Console.WriteLine(name);
```
## Format the String
ممكن نستخدم `String.format`
```cs
string str = String.Format("Hello World {0}", x);
// You can use it at Output
Console.Write(String.Format("Hello World {0}", x));
```

We can use also `$` string interpolation
```cs
string str = $"Hello World {x}";
```

We can use `@` verbatim, to output raw text 
```cs
Console.WriteLine($@"C:\Output\{projectName}\Data");
```
## Access Strings
ممكن نوصل لأي عنصر في ال string من خلال ال index
```cs
string myString = "Hello";
Console.WriteLine(myString[1]);  // Outputs "e"
Console.WriteLine(myString[0]);  // Outputs "H"
```

ممكن نستخدم  method اسمها `IndexOf()` عشان أعرف ال index بتاع أي عنصر في ال string
```cs
myString.IndexOf("e"); // 1
```

فيه method كمان جميلة أوي اسمها `SubString()` عشان تجيبلك string من واحدة قديمة من خلال أول index لحد الآخر
```cs
// Full name
string name = "John Doe";

// Location of the letter D
int charPos = name.IndexOf("D");

// Get last name
string lastName = name.Substring(charPos);

// Print the result
Console.WriteLine(lastName);
```

## Empty String
في بعض الأحيان ببقا عايز string فاضية عشان أحط فيها القيم اللي هتطلع 
في الحالة دي ممكن نستخدم `string.Empty`

```cs
string number = string.Empty;

for (int i = 0; i < 10; i++)
{
	numbers = numbers + i.ToString();
}
```