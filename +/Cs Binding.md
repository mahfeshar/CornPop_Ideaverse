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

إني أعمل Reference يشاور على Child للـ class اللي بعمل منه Reference
بمعنى إني أقدر بالـ Reference للـ Class أشاور على نفس الـ Class أو Child له
```cs
// Parent      Child
TypeA T1 = new TypeB(1, 2);
// Reference from Parent --> Object from Child
```
- مش بيشوف غير الجزء اللي الإبن **وارثه من الأب** بس غير كدا مبيشوفش
- هو عبارة عن [[Cs Value and Reference Types#Reference Types|Reference Type]]
	- الـ Reference اللي هو العنوان هيروح في الـ Stack والـ  Object نفسه أو القيمة في الـ Heap
	- `TypeA T1 = new TypeB();`
	  Reference                 Object
## Override
- عرفنا ان فيه طريقتين للـ Override هنا [[Cs Polymorphism#Overriding]] 
- لو عملت override عن طريق new هينفذ أول Function عندي بتاع الـ Parent مش هيشوف الـ Override الجديدة وهيعتبر دي Function جديدة بينفرد بيها الـ Child
- إنما لو بكلمة override هينفذ اللي انت عملته فالأخر وهينفذها (بتاع الإبن)