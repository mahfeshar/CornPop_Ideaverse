---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-07-21
---

![[Pasted image 20240511115224.png]]
## Linear (procedure) code
- كان فيه تكرار بطريقة كبيرة جدًا
- بيعمل مشكلة لو العميل لو حب يغير أو يعدل في الكود بيبقا **مكلف جدًا** 
  والكود بيبقا اسبكيتي كود فلو غيرت سطر هيغير في كله وا لكود هيبوظ
- مكنش فيه function ولا class ولا object والكود عبارة عن single block code
## Structure programming (Function)
- بدأ يظهر مصطلع ال Function Programming وبدأنا نقسم الكود عن طريق ال Function
- ال Function تقدر تعمل كول لبعضها ودا كان عن طريق لغة ال C في الوقت دا
- فيها عيوب زي:
	- Global variable
	- Stand alone function (فانكشن مش تابعة لأي حد ومش موجودة في كلاس)
## OOP
- الوحدة الأساسية بتاعته هي الـ class ومن خلاله حلينا العيوب اللي قبل كدا 
- ال OOP عبارة عن class و بيحتوى على methods, data
### قصة اختراع الـ C#
- أول لغة طلعت كانت **Smalltalk** ووقتها كان صعب اني اشتغل بلغة ال C واغير للغة  تانية زي اللغة دي
- فعملوا لغة تانية وهي ال C++ فهي نفس ال C وزودوا عليها ال OOP
- ال C++ في الحقيقة هي ==Not pure OOP== 
  لأن جواها تقدر تكتب بلغة ال C وتقدر تكتب OOP 
  فبالتالي أقدر أكتب Stand alone function and global variable
- بعد كدا شركة Sun عملت لغة Java وخدو C++ وخلوها Pure OOP يعني مقدرش أكتب Global variable, Stand alone function وبعدها شركة اوريكال اشترت شركة Sun
---
- مايكروسوفت كانت عايزة تعمل لغة Pure OOP فخدت ال C وال C++ 
  وعملت لغة اسمها Cool (C like object oriented language) فالاسم مكنش حلو في السوق فعملوا C++++ فمكنش حلو برضو 
  من هنا ظهر اسم C# فالشباك عبارة عن أربعة + فوق وجنب بعض
- ال C# اتعملت سنة 2000 وتاني فيرجن اتعملت 2005 وهي Pure OOP يعني ايه؟ صح كدا

## مثال للفرق بينهم
![[00 Programming Paradigms.png]]
- نفترض ان احنا قاعدين على سفرة أكل وعندي أكلات معينة (Methods)
- هتلاقي ان الشخص A عايز لحمة و B محتاج فاكهة فدا هيعمل لغبطة وهيبوظ الدنيا برضو
- انما لو غطيت كل حاجة من دي وعشان أستخدمها لازم إذن (getter and setter) فدا هيخلي الدنيا ملمومة شوية
## Namespace
- الناس بعد ما جمعوا الكود في functions جوا classes ليها علاقة ببعض قالوا برضو لازم نجمعهم تاني
- عملوا namespace أو package أو `dll` (Dynamic Link Library) ودي بتجمع classes مع بعض 
- حتى ال dotnet نفسها هي عبارة عن namespaces كتير اللي هي زي ال packages 
  وال namespace ممكن يبقا جواه أكتر من namespace وهكذا
- ومجموعة ال namespaces بيتقال عليهم assembly اللي هو البرنامج بتاعي في الأخر

```cs
System.Console.WriteLine()
namespace.class.function()
```