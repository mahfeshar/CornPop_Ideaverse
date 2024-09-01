---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-20
tags:
  - fcdotnet/access
---

- عبارة عن C# Keywords بتساعدني اني اعمل Indicate the accessibility scope

- أنا جوا ال [[Cs Namespace|Namespace]] بكتب أربع حاجات: 
  Class - Interface ([[Cs Value and Reference Types#Reference Types|Reference Types]]) | Struct - Enum (Value Type)
  وبرضو جوا الحاجات دي بيبقا فيه حاجات تانية زي فانكشنز او متغيرات وهكذا
  محتاج أعرف الحاجات دي هتبقا Accessible لحد فين بالظبط سواء جوا ال Library بس ولا لو حد استخدم ال Library في بروجكت تاني

![[Pasted image 20240803103104.png]]
## Inside [[Cs Namespace|Namespace]]
بنقدر نكتب جوا ال Namespace أربع حاجات:
1. [[Cs Class]]
2. [[Cs Struct]] stands for structure
3. [[CSharp Interface]]
4. [[Cs Enums]]

---
معنديش Access Modifiers غير اتنين جوا ال Namespace:
1. Internal (**Default**)
2. Public

>قبل ما تحاول تستخدم أي class أو حاجة موجود في ==Library== تانية لازم إني أضيف ال Library دي للـDependences للبروجكت
  Right click at project -> Build dependencies -> Project dependencies
  Add project reference
  وبعد كدا أعمل using للـLibrary دي
### Internal
- قولنا اننا لو مديناش الحاجة Access Modifier فهو طبيعي هيبقا Internal 
- معناها إني هي ليها Access بس جوا ال Library اللي انا فيها 
  ولو حاولت أعملها Access جوا Library أو بروجكت تاني مش هينفع ومش هقدر أوصله
- لو حاولت أوصل ل class مثلًا في project مختلف هيديلي error
- الحل إنك تعملها public عشان تقدر توصلها في أي Project وأي Library مختلفة


## Inside [[Cs Class|Class]] or [[Cs Struct|Struct]]
بنقدر نكتب جواهم:
1. Attributes (Fields) -> Member Variables
2. [[CSharp Property]] (Full Property, Automatic Property, Indexer -> Special)
3. [[CSharp Function]] (Constructor, Getter Setter, Method)
4. [[CSharp Event]]

---
متاح 3 Access Modifiers جوا الـ **Struct**: (نفس بتاع الـ Name Space وهنزود الـ Private)
1. Private (Default)
2. Internal
3. Public

جوا الـ **Class** متاح كل الستة:
1. Private (Default)
2. Private Protected
3. Protected
4. Internal
5. Internal Protected
6. Public

> [!example] Default
> الـ Default فيهم الإتنين هو **Private**

### Private
- الـ Member بيبقا عليه قفل كدا
- مش بيبقا متاح برا الـ Scope اللي انا فيه سواء Class أو Struct

### Internal
- بيبقا عليه علامة قلب
- متقدرش تشاركه برا الـ Project بتاعك
  بمعنى انك لو عملت Library معينة فدي Project تقدر جواها تستخدم الـ Member لو Internal إنما لو استدعيته جوا Project تاني مش هيرضى
## Inside [[CSharp Interface|Interface]]
نقدر نكتب جواها:
1. Signature for Property
2. Signature for Method
3. Default Implemented Method (فانكشن كاملة)

الـ Method بتتكون من جزئين (Signature - Body):
الـ Signature اللي هو اسمها والـ Parameters اللي بتستقبلها وكدا

> [!example] Default
> الـ Default فيها هو **Public**
> لأن بكتب فيها signatures فمحتاج أوصل للـ Implementation

## Inside [[Cs Enums|Enums]]
بنكتب جواها Labels

## Flashcards
ايه هي الـ Access Modifiers
?
عبارة عن C# Keywords بتساعدني اني اعمل Indicate the accessibility scope

---
كم عدد الـ Access Modifiers وقولهوملي
?
عددهم 6
Private - Public - Internal - Protected - Private Protected - Internal Protected

---
نقدر نكتب ايه جوا الـ Namespace وايه الـ Access Modifiers المتاحة وايه الـ Default
?
Class - Interface - Struct - Enum
متاح 2 وهما الـ Internal و الـ Public
والـ Internal هي الـ Default

---
نقدر نكتب ايه جوا الـ Struct و Class وايه الـ Access Modifiers المتاحة وايه الـ Default
?
1. Attributes (Fields) -> Member Variables
2. CSharp Property (Full Property, Automatic Property, Indexer -> Special)
3. CSharp Function (Constructor, Getter Setter, Method)
4. CSharp Event
متاح 3 Access Modifiers جوا الـ **Struct**: (نفس بتاع الـ Name Space وهنزود الـ Private)
1. Private (Default)
2. Internal
3. Public
جوا الـ **Class** متاح كل الستة:
1. Private (Default)
2. Private Protected
3. Protected
4. Internal
5. Internal Protected
6. Public

---
نقدر نكتب ايه جوا الـ Interface وايه الـ Default
?
نقدر نكتب جواها:
1. Signature for Property
2. Signature for Method
3. Default Implemented Method (فانكشن كاملة)
الـ Default فيها هو **Public**
لأن بكتب فيها signatures فمحتاج أوصل للـ Implementation

---
نقدر نكتب ايه جوا الـ Enum:: بنكتب جواها Labels