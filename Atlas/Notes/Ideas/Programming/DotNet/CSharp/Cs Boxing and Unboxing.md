---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-06
---
We talked before about [[Cs Data Types]] and how this data stored in memory at **Stack** or **Heap**

---
- The C# Type System contains three data types: **Value Types**, **Reference Types** and **Pointer Types**.
- Basically, **Boxing** converts a Value Type variable into a Reference Type variable, and **Unboxing** achieves the vice-versa.

---
## Boxing
- بحول ال Value Type (Stack) إلى Reference Type(Heap)
- بتخلي حاجة بتتخزن في Stack تروح تتخزن في ال Heap
- We will use in this method [[Cs System.Object]] (Super type)
```cs
int num = 23; // Value Type
Object Obj = num; // Value(int) -> Reference(object) : Boxing
```

![[Pasted image 20240706121625.png]]
بتفقد كل مميزات الحاجة اللي بتعملها Boxing 
```cs
int x = 5;
object o = x; // Boxing

int y = x + o; // ERROR
int z = (int) o; // Unboxing
```
عشان تقدر تستخدمه تاني لازم تعمله Unboxing تاني
## Unboxing
- عكس العملية اللي فاتت
- بحول ال Reference Type(Heap) إلى Value Type (Stack)
```cs
Obj = 123;
num = (int) Obj;
```
- We use with it [[Cs Type Casting#Explicit Casting|Explicit Casting]]
![[Pasted image 20240706121701.png]]
## Performance
العمليتين دول هما عمليتين Expensive فمتستخدمهمش كتير