---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-08-03
tags:
  - fcdotnet/struct
---

دا عبارة عن [[Cs Value and Reference Types#Value Types|Value Types]]

```cs
// default access modifier inside Namespace : internal
// internal vs Public
struct TypeA
{
	int X;
	// Default access modifier: Private
	public void Print ()
	{
		Console.WriteLine(${X});
	}
}

public struct TypeB
{
	//code
}
```

- لو روحت على project تاني وعايز أستخدم ال struct اللي انا عامله دا مش هيرضى اني اعمل using للـ namespace اصلا ؟
	لازم الأول تضيفها في ال dependencies -> add project reference 

- ال datatype زي ال struct برضو ليها access modifier جوا ال namespace فلازم تحدد برضو هو public

```cs
// Point is a struct
Point p1; // P1 is Object for the point struct
// Allocation 8 Uninitialized bytes in Stack : Value type
Console.WriteLine(p1);//error: Garbage 
```
- مش بيتعمل reference  انما لما بنستخدمه بنعمل منه Object 
  على عكس الـ Class كان بيعمل Reference
- بمعنى إن الـ CLR هيخزن في الـ Stack المساحة بتاعته اللي محتاجها 
- طيب ليه بنستخدم الـ new معاها ودا عشان نحدد هنستخدم أنهي Constructor وتختاره
```cs
P1 = new Point()
// new is just only for constructor selection
// That will initialize the attributes of the object
```
### Access Modifier
اتكلمنا عنها بالتفصيل في [[Cs Access Modifiers#Inside CSharp Class Class or CSharp Struct Struct|Inside Struct]]
### Constructor
 - اتكلمنا عنه بالتفصيل في [[Cs Constructor]]
 - اقدر اعرف multiple constructors
 
```cs
struct Point
{
    int X, Y;

    //User defined ctor
    public Point(int _X, int _Y)
    {
        X = _X;
        Y = _Y;
    }

	public Point(int N)
	{
		X = Y = N;
	}

	// Parameterless ctor
	// By default, we have this ctor
	public Point()
	{
		X = Y = 0;
	}
    // وارث من system.object
    public override string ToString() // overriding
    {
        return $"({X},{Y})";
    }
}

Point P2 = new Point(10, 15);
//P2 allocated in Stack
//use new keyword just for Ctor selection
Point P3 = new Point(15);

```

## Flashcards
بنستخدم الـ Struct ليه؟ :: لتجميع البيانات ذات الصلة معًا ونعمل نوع جديد وهو شبه كتير الـ  class

---
ايه الفرق بين الـ Class و Struct؟  ^8c8987

?

| Feature     | Struct                                 | Class                                     |
| ----------- | -------------------------------------- | ----------------------------------------- |
| Type        | Value Type                             | Reference Type                            |
| Inheritance | لا يدعم                                | يدعم                                      |
| Memory      | يتم تخزينها في الذاكرة المؤقتة (stack) | يتم تخزينها في الذاكرة الديناميكية (heap) |
| Efficient   | يمكن أن يكون أكثر كفاءة                | قد يكون أقل كفاءة في بعض الحالات          |

---
ايه الـ Default access modifier له وللي جواه؟
?
default access level inside: Private
default access level for it: internal

---
الـ Access Modifier بتاع الـ ctor جواه بيبقا دايمًا {{public}} إلا في {{حالة واحدة}}

---
نقدر نكتب ايه جوا الـ Struct وايه الـ Access Modifiers المتاحة وايه الـ Default
?
1. Attributes (Fields) -> Member Variables
2. CSharp Property (Full Property, Automatic Property, Indexer -> Special)
3. CSharp Function (Constructor, Getter Setter, Method)
4. CSharp Event
متاح 3 Access Modifiers جوا الـ **Struct**: (نفس بتاع الـ Name Space وهنزود الـ Private)
1. Private (Default)
2. Internal
3. Public

---
ليه بنستخدم new معاها وايه دلالتها
?
- مش بيتعمل reference  انما لما بنستخدمه بنعمل منه Object 
  على عكس الـ Class كان بيعمل Reference
- بمعنى إن الـ CLR هيخزن في الـ Stack المساحة بتاعته اللي محتاجها 
- طيب ليه بنستخدم الـ new معاها ودا عشان نحدد هنستخدم أنهي Constructor وتختاره

---
