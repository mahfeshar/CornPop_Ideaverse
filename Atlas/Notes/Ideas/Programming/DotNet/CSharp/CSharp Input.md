---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-06
---

## Get User Input
- We use for this `Console.ReadLine()`
- الداتا بتتخزن بنوع [[CSharp String]]
```cs
String userName = Console.ReadLine();

Console.WriteLine("Username is: " + userName);
```
## User Input and Numbers
طب لو أنا عايز  أدخل رقم في الحالة دي هيرفض
```cs
int age = Console.ReadLine(); //ERROR
```

We should make [[CSharp Type Casting#Explicit Casting|Explicit Casting]]

```cs
int age = Convert.ToInt32(Console.ReadLine());
```

---
```cs
Console.ReadLine(); // Always take string so you should parse (casting)
DateTime BirthDate = DateTime.Parse(Console.ReadLine());
```
- في الحالة دي لو دخلت data type مختلفة غير اللي انت محول ليها كدا هيطلعلك error
- You should handle [[CSharp Handle Exception]]

