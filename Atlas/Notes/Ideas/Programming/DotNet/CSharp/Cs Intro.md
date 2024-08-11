---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-01
---

 - We have Folder per **Solution** 
   and inside it, We have `sln` file just configuration file for my solution and projects
- Inside solution, We have folder per **every project**

- And inside project, We have also configuration file for project
- we can change some Properties for project by (right click it -> Properties)

- To add file, That I should write could in it (add -> class)

---
## C# Syntax
- أي حاجة في ال .Net هي عبارة عن pure oop فدايمًا هتلاقي نفسك بتستخدم ال Classes 
- فعشان كدا ال function (main) مينفعش تتكتب في الهوا، لازم تتكتب جوا class

- وقبل ال class لازم أعرف ال namespace 

- وجوا ال class ببدأ أعرف ال main function بتاعتي
  ولازم تبقا static void عشان دي ال startup بتاعتي اللي هي أول حاجة هنفذها

- وافتكر ان اللي بينادي ال main هو ال CLR اللي اتكلمنا عليه في [[DotNet Story]] فعشان يندهلها يعرف يندهلها على طول مش يعمل object من class ال main وبعدها يندهلها

```cs
namespace HWNS
{
    class Program
    {
        public static void Main()
        {
            System.Console.WriteLine("Hello World");
        }
    }
}
```

`namespace` is used to organize your code, and it is a container for classes and other namespaces.

وشرح ال [[Cs Output#|WriteLine]] هنا
### using 
- لما تلاقي عندك datatype مش موجودة على مستوى ال namespace HWNS روح دور عليه ف ال namespace اللي اسمه System
- It means that we can use classes from the `System` namespace
```cs
using System;
namespace HWNS
{
	class Program
	{
		public static void Main()
		{
			Console.WriteLine("Hello World!")
		}
	}
}
```

- فيه بعض ال namespaces بتبقا متعرفة global تلقائي في فايل اسمع global using 

![[Pasted image 20240701103700.png]]
## Important
- Case sensitive
- Pascal Case (BackgroundColor)