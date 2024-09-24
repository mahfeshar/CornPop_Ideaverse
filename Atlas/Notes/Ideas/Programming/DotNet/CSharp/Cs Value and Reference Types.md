---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-04
---
We talked about [[CLS and CTS]], Read it again
## Memory

![[Heap & Stack.png]]
- الmemory فيها أكتر من مكان بيتم استخدامهم
- الأماكن اللي بيتخزن فيها ال variables اسمها Stack, Heap
### Stack
- مكان في ال memory بيبقا محدود بس بيبقا سريع جدًا لما بتخزن فيه حاجة
- بيتخزن فيه ال Value Types وعناوين ال Reference Types اللي بتتخزن في ال Heap
- ممكن يتملى عادي جدًا وبيبقا ايرور اسمه Stack Overflow عشان كدا لازم تاخد بالك من النقطة دي
### Heap
- المكان دا بيتخزن فيه برضو variables بس الفكرة إنه بياخد مساحة ال RAM كله فصعب إنه يتملى
- بيتخزن فيه ال Reference Types (الداتا) والعنوان بتاعها بيروح يتخزن في ال Stack
- مفيش ايرور اسمه Heap Overflow
- ال Garbage collector بيشتغل عليها بس بيشتغل يدوي
## Value Types

- انت أول ما بتعرفها بيروح على طول في ال memory يحجز مكان 
- ولما تديلها قيمة يبعت القيمة دي على المكان اللي في ال memory دا 
  والمكان دا اسمها **Stack**

- بيبدأ يحجز مكان في ال memory لما بتديله قيمة غير كدا مبيدخلش (مشكوك في أمر هذا الكلام)

- ال struct وال enum يعتبرو value types 
  اعرف برضو ان الاتنين دول *لا بيورثوا ولا بيورثوا*

- كل ال built-in يعتبروا value types ما عدا كام حاجة بس زي ال string و System.Object
[[Cs Data Types#Bulit-in types table (Primitive)]]

```cs
int X; // int: c# keyword 
// Allocation of 4 uninitialized Bytes in Stack
X = 5; // put 5 at the allocated bytes

Int32 Y; //Another way to define the integers
//Int32: BCL (IL code)

y = x; // At Y location we put the value of X
++x; // x increased by 1 
// x = 6, y = 5
```

![[Pasted image 20240310160848.png]]
- مش بتسمح بال *null* 
  ممكن تاخد قيمة [[Cs Null]] عن طريق ال [[Cs Null#|Nullable Types]]
### access garbage
- ال c# مش بتسمح انك تعملها access وبتديك ايرور على عكس اللغات التانية اللي كانت بتطلعلك قيمة
- أصلًا لو مديتلهاش قيمة مش بيتحط قيمة garbage، بس بتبقا **مش موجودة** أصلًا
```cs
int x;
WriteLine(x) //error
y = x // error
```

### Stack
- دا اللي بيتخزن فيه الداتا عادي وخد بالك بيخزن ال data مش عنوان ليها أو حاجة
- كل var بيبقا له Index معين
- ممكن يتملى مع الوقت على عكس ال Heap وبيعمل (Stack Overflow)

## Reference Types
- مش بيحجز مكان في ال memory، هو حاجة أشبه باسم الدلع او alias مش أكتر
  بيحجز قيمته في ال Heap وبيباصي العنوان لل Stack

- لو عايز تحجزله مكان بقا بنستخدم كلمة `new` وبعدها هيبدأ **يخزن الداتا فعلًا** بس بيخزنها في ال *Heap*
  أول ما بستخدم كلمة new بحجز مكان بالفعل وبيحطله initial value على حسب نوع الداتا أو من خلال الـ [[Cs Constructor]] 
  مثال: لما باجي أعمل Array جديدة [[Cs Arrays#Create an Array|Create Array]]
- عشان أقدر أناديله لازم يبقا في ال stack عشان كدا هو بيخزن ال address بتاع ال object في ال stack
- لما بتبدأ تحدد new بيحط default value في الحاجة اللي انت حددتها دي

- ال class, **String** يعتبر reference type
- ودا بسبب إن ال string ملوش مساحة محددة

- بتسمح بال `null` عادي

- نتكلم الأول عن [[Cs System.Object]] 
```cs
Object o1; // zero bytes have been allocated in Heap

o1 = new Object();
// new(IL -> newObj)

Object o2 = new Object();
o2 = o1;
```

- هنا بقا لما شاورت على ال `o1`، ال object التاني هيروح يشاور على نفس الحتة في الheap والحتة اللي كان خزنها بتبقا مفيش حاجة بتشاور عليها 
- *ملحوظة*: ال reference عامل زي ال pointer بس بشكل كتابة مختلف وبتعمل نفس الوظائف
![[Pasted image 20240310165514.png]]

### New
لما بكتب new دا اللي بيحصل
1. Allocate Required number(#) of Bytes in Heap (Object Size + CLR Overhead Variables)
	- أي حاجة بتحطها في ال Heap بيبدأ ال CLR بيحط اتنين variables عشان يستخدمهم 
	- بيحط 64 bit لكل variable 
	- فكدا بيبقا فيه 16 byte زيادة على أي حاجة بتتخزن في ال heap
2. Initialize (cross out) allocated Bytes with default value
3. Call user defined **constructor** if exists
4. Assign reference (address of the allocated object at heap) to new key allocated Object
### Garbage Collector
- طبعا زي ما قولنا فوق لما بتشاور على حاجة تانية الحاجة اللي كنت مشاور عليها في الاول دي بتبقا **unreachable location** ومبتقدرش توصلها وبتعتبر garbage 
  بس انت هنا مش بتشيل هم انك تمسحها بايدك وتنظفها
- فهنا بتيجي وظيفة ال **garbage collector** اللي بتعدي على ال heap وبتبدأ تشوف أي garbage تمسحها بشكل تلقائي 
---
- لو ال heap قرب يتملى بيبدأ ال CLR يلاحظ الحوار دا فبينادي على الgarbage collector
- وفي اللحظة دي البرنامج بتاعي بيقف **عشان كدا هيفرق معايا ان اعرف انه بيشتغل ازاي**
- هو بيقف فترة صغيرة جدًا بس الموضوع لو *اتكرر كتير* هيقلل ال performance 
- فانت لازم وانت بتعمل locate لحاجة في الheap تفتكر الحوار دا ومتعملش غير الحاجات الضرورية بس
---
- افتكر اني قولت فوق على ال struct, enum انهم **مش بيورثوا** انما ال class بيورث ل single parent بس 
- فانت اعمل حسابك لو حاجة هتورث قدام تستخدم ال class (reference) 
  لو غير كدا تستخدم الحاجات التانية