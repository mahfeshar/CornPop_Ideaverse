---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-08-03
tags:
  - fcdotnet/enum
---

- عبارة عن datatype انت اللي بتحدد ال values اللي ممكن ياخدها 
- هو Object أقدر أعمل عليه Loops
- بعرفها جوا الـ [[Cs Namespace]] 
- تعتبر [[Cs Value and Reference Types#Value Types|Value Types]]
- بيحسن ال readability بتاع الكود وبيقلل ان انت وزمايلك اللي شغالين على نفس البروجكت تغلطو
- هو اعادة تسمية لبعض القيم ال int وبتديلها أسامي، يعني محجوز في الmemory في 4 byte 
- بنكتب جواه Labels

- بستخدمها لما يبقا عندي مجموعة من الـ Values وعايز اعملهم Data Type خاصة بيهم 
  بمعنى اني عارف ان الأرقام بحطها في الـ Int مثلًا بس لو بخزن نوع الجنس Gender فهو M, F فهنا نعملها data type خاصة بيها
### Enum Example
```cs
enum Grades
{
	A, B, C, D, E // Labels: may be word or smth
}

enum Gender
{
	Male = 1, Female = 2, M = 1, F = 2
}

//Main
Grades myGrade = Grades.A;
myGrade = Grades.C;

//int
myGrade = 2; // error
myGrade = (Grades) 2; //explicit : myGrade = Grades.C

// لو اديتله قيمة مش موجودة بيطبع الرقم
myGrade = (Grades) 8; // output: 8

switch (myGrade)
{
	case Grades.A:
		break;
}
```
قولنا انها بتتعامل بالـ Labels بس الـ CLR مش بيتعامل بيها فبيدي لكل Label منهم رقم
### Enum Values
اقدر أغير ال default values اللي بتتحط لكل label
```cs
enum Branches
{
	SV = 105, NasrCity = 201, Alex  = 221, Assuit
	//Assuit = 222
	// We can use it with IDs
}

// Main
Branches MYB = new Branches(); // Default int: 0
MYB = Branches.Alex;
```
### Size for Variables 
بياخد 4 byte زي ما قولت لأنه بيعتبر `Int` بس انا في المثال اللي فوق مش محتاج كل دا انا بخزن 0 1 2
```cs
enum Branches:byte // Inhertince but I don't mean here inher
{
	//Labels
}
```
- بقوله ببساطة خلي النوع اللي بيتخزن `byte`
### Bit Flags with Enum
- لو عايز مثلًا أخزن خصائص لخط معين هل هو  bold ولا لا، italic, underline
	فالحل الممكن اني أعمل array of Booleans واخزن فيه القيم دي وكل index بيمثل حاجة معينة
```cs
bool[] Flages = new bool[4];
```
- **عيوبها:**
	- لو عايز أغير كل القيم اللي جواه اني أخلي كل الخصائص دي تتغير فهحتاج أستخدم for loop وبكدا ال time هيبقا O(N) 
	- وكمان انا محتفظ في ال memory لل array كلها 4 bytes

![[Pasted image 20240319111406.png]]

- فبدل ما بعرف 4 bytes عشان أعمل الحوار دا ممكن أستخدم 1 byte اني اعمل كل دا عن طريق استخدام ال bit 
- وكمان هيديلي ميزة اني أقدر اغير كله ب O(1) ودا عن طريق استخدام ال bitwise operations من غير loop ولا حاجة
![[Pasted image 20240319111431.png]]
![[Pasted image 20240319111439.png]]
#### Permissions Example
```cs
[Flags] // Attribute : Like decorator in Angular 
// (Just tell the compiler what is this?)
// لو ملقاش ليبل بيمثل الرقم بيحاول يجيب اللي بيجمعهم كلهم سوا
enum Permisions:byte
{
    Read = 8, Write = 0x04, Excute = 0b_0000_0010, Delete = 1, RootUser = 15
    // We can set it with any Form, it doesn't matter
}

//Main
Permisions PRM = new Permisions();
Console.WriteLine(PRM); // 0

PRM = Permisions.Read;
Console.WriteLine(PRM); // Read

PRM ^= Permisions.Write; // XOR: عشان اعكس
Console.WriteLine(PRM); // With flags: Wrtie, Read ; without: 12

PRM |= permisions.Execute; // OR : To add new one
PRM &= ~(permisions.Execute); // NAND : To remove

PRM = (Permisions)15;
Console.WriteLine(PRM);
// Without RootUser: Delete, Excute, Write, Read
// With : RootUser

// Check if We can write
// AND : To check
if((PRM & Permisions.Write) == Permisions.Write) 
    Console.WriteLine("True"); // True
```

### Enum Parsing
We talked before about [[Cs Type Casting]]

---
Create an enum called "Season" with the four seasons (Spring, Summer, Autumn, Winter) as its members. Write a C# program that takes a season name as input from the user and displays the corresponding month range for that season. Note range for seasons ( spring march to may , summer june to august , autumn September to November , winter December to February)

```cs
using System;

enum Season
{
    Spring,
    Summer,
    Autumn,
    Winter
}

class Program
{
    static void Main()
    {
        Console.WriteLine("Enter a season (Spring, Summer, Autumn, Winter):");
        string userInput = Console.ReadLine();

        try
        {
            // Parse the user input to a Season enum value
            Season season = (Season)Enum.Parse(typeof(Season), userInput, true);

            // Display the corresponding month range for the entered season
            switch (season)
            {
                case Season.Spring:
                    Console.WriteLine("Spring: March to May");
                    break;
                case Season.Summer:
                    Console.WriteLine("Summer: June to August");
                    break;
                case Season.Autumn:
                    Console.WriteLine("Autumn: September to November");
                    break;
                case Season.Winter:
                    Console.WriteLine("Winter: December to February");
                    break;
                default:
                    Console.WriteLine("Invalid season.");
                    break;
            }
        }
        catch (Exception)
        {
            Console.WriteLine("Invalid input. Please enter a valid season name.");
        }
    }
}

```
## Flashcards
ايه هو الـ Enum
?
عبارة عن datatype انت اللي بتحدد ال values اللي ممكن ياخدها 

---
بتتعرف جوا {{Namespace}}

---
هي عبارة عن {{Value}} Type

---
الـ Compiler بيفهم الـ Labels وبيتعامل معاها عادي؟ :: لا، بيحولها ل Int بالترتيب وممكن تغير لأي نوع تاني بالـ Inheritance