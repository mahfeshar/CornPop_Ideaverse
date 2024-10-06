---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-06
---
```cs
TypeA T1 = new TypeA();
TypeB T2 = new TypeB();
// Not Binding: Reference from Parent --< object from Parent
```

- إني أعمل Reference يشاور على Child للـ class اللي بعمل منه Reference
- بمعنى إني أقدر بالـ Reference للـ Class أشاور على نفس الـ Class أو Child له
```cs
// Parent      Child
TypeA T1 = new TypeB(1, 2);
// Reference from Parent --> Object from Child
```
- مش بيشوف غير الجزء اللي الإبن **وارثه من الأب** بس غير كدا مبيشوفش
- هو عبارة عن [[Cs Value and Reference Types#Reference Types|Reference Type]]
	- الـ Reference اللي هو العنوان هيروح في الـ Stack والـ  Object نفسه أو القيمة في الـ Heap
```cs
TypeA T1 = new TypeB();
// Reference   Object
// Address     Value
// Stack       Heap
```
## Override
- عرفنا ان فيه طريقتين للـ Override هنا [[Cs Polymorphism#Overriding|Override]] 
الـ **Static Binding** (Early Binding): 
- لو عملت override عن طريق new هينفذ أول Function عندي بتاع الـ Parent مش هيشوف الـ Override الجديدة وهيعتبر دي Function جديدة بينفرد بيها الـ Child
- Compiler will bind function call based on **Reference Type**  NOT Object Type at **compilation Time**
الـ **Dynamic Binding**: 
- إنما لو بكلمة override هينفذ اللي انت عملته فالأخر وهينفذها (بتاع الإبن)
- CLR will Bind Function Call based on **Object Type** NOT Reference Type at **Run Time**
## Not Binding
مثال:
- لو عندي كلب أقدر أقول عليه إنه حيوان 
- بس مش كل حيوان هقدر أقول عليه انه كلب
- عشان كدا كنا بنستخدم [[Cs Type Casting]] في الحالة اللي زي دي

```cs
// Dog = Animal // مقدرش
// Dog = (Dog) Animal // الحيوان دا بوعدك انه كلب

object O1 = 3;

// int x = O1; // ERROR
// Cause
// O1 = "Ahmed"; // Object can be anything
int x = (int) O1; // بوعدك هيبقا انتجر
//
```