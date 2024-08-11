---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-05-12
tags: []
---
## Pre DotNet
![[Pasted image 20240511120352.png]]
- قبل 2002 مايكروسوفت عملت `Delphi`, `VB`, `Visual Cpp`، بس فكرت تعمل DotNet بسبب مشكلتين:
	1. مقدرش أعمل برنامج يشتغل على كل البلاتفورم المختلفة Can't create **cross platform app**
	2. مقدرش أشتغل في نفس البروجكت بأكتر من لغة No cross language 
- عشان نوضح دا لازم نقول ال Life cycle قبل ال DotNet كان عامل ازاي
	- عايز أعمل برنامج فكتب الكود بتاعي 
	- الكومبايلر بياخد الكود ويحوله ل Native code اللي هو 0,1  ودا بنسميه ==platform dependent==
		- بيعتمد على ال platform اللي بيتترجم عليه البرنامج ودا لأن ال structure بتاع كل بلاتفورم مختلفة عن التانية
## With DotNet 2002
- DotNet Framework: is a Big Container for software technologies like Web (ASP), Mobile (Xamrin), Desktop (WPF). ==إطار عمل==
بيتكون من حاجتين:
1. الـ Libraries اللي فيها الحاجات بتاعت كل تكنولوجي من دول ASP, WPF, Xamrin 
   ودا يسمى ب BCL (Base class library of technologies)
   زي الـ String هو كلاس موجود في مكتبة اسمها System اللي هي من ضمن الـ BCL

2. الـ CLR (Common language runtime) وبيتكون من 3 حاجات:
	1. لغات ال DotNet واشهرهم C#
	2. الكومبيلر بتاع كل لغة يعني مثلًا بتاع C# اسمه Roslyn
	3. الـ Runtime Components

![[Pasted image 20240511153231.png]]
## .NET Code Compilation steps
![[Pasted image 20240511153630.png]]
1. بكتب الكود بتاعي وبعد كدا بتحصل عملية ال Compilation 
   باستخدام الكومبيلر بتاع C# اللي اسمه Roslyn 
2. بيحول الكود لحاجة اسمها CIL (Common Intermediate Language), IL, MSIL (Microsoft)
   ودا بيكون عبارة عن فايل اسمه assembly file وبيكون امتداده `dll` (Dynamic link library) 
   دا ملوش علاقة بالـ assembly العادي، دا مجرد IL بس (مجرد تشابه أسماء)
3. الفايل بيكون Platform independent 
   يعني لو عملت Compile على أي بلاتفورم تاني هيطلع نفس فايل ال IL
   الفايل دا مش هيأكل عيش عشان الكمبيوتر مبيفهمش غير machine code (exe)
4. بيدخل عملية ال runtime 
   عندنا حاجة اسمها JIT compiler (just in time) بياخد ال IL ويحوله لـ native code (exe) ودا بيسموه SDK في ال C#

> [!danger]
> لسا المشكلة بتاع cross platform متحلتش في الـ .NET Framework لأن كل platform (Linux, Mac, win) المفروض يبقا ليهم الـCLR الخاص بيهم وليهم الـ JET compiler الخاص بيهم عشان يعمل المرحلة الأخيرة دي على جهازة والبرامج تشتغل فمايكروسوفت المفروض تعمل لكل platform SDK خاص بيها فيه الـ Compiler بس دا محصلش  

> [!banner-image] SDK
> Software Development Kit
> هو مجموعة الأدوات والمكتبات اللي بتسهل الـ Development وبيبقا فيه حاجات كتير:
> - Compiler
> - Libraries
> - Tools (Like CLI)
> - Templates
> - Runtime (.NET Core or .NET Framework)

> [!info] Runtime vs Compilation
> - الـ compilation: هي عملية تحويل الـ code لـ IL وبنسخدم فيها compiler زي Roslyn ودا اللي بيظهر فيه الـ Compilation errors
> - الـ Runtime: عملية تحويل الـ IL إلى Native (exe) ودي بنستخدم فيها ال JIT وبيظهر فيه الـ Runtime error

---
- الفرق في ال Life cycle قبل وبعد هو الـ JIT ودا هيعملي overhead in runtime وهيبطأ الـ Runtime شوية

عشان يحلو المشاكل دي:
1. ال JIT خلاه 64bit ودا أسرع
2. ال Jitting بيحصل مرة واحدة لما بعمل call function وطالما أنا مقفلتش البرنامج هيفضل زي ما هو ومش هيحتاج يعمل تاني


>[!Note]
> عندنا وقتين في ال Life cycle وهي عملية الكومبيلر ل IL وال JET compiler ودا ال .net Framwork القديم

دا مش حل كامل للأسف فحلينا المشكلة التانية وهي اني أكتب بأكتر من لغة برمجة بس المشكلة الأولى لسا متحلتش
## .NET Core
- اتعمل في 2014 واتغلب على المشاكل السابقة وظهر للناس في 2016
- قبلها كان فيه تيم من الديفولبرز شغالين على حاجة اسمها Mono Project/framework وهو عبارة عن حل لمشكلة ال Cross platform اني أكتب الكود على أكتر من حاجة ويشتغل عليهم 
  كانت حاجة مش رسمية فمكنش فيه سابورت وكان بيبقا دايمًا متأخر version عن DotNet Framework 
- عشان كدا عملوا ال .NET Core

![[Pasted image 20240511160011.png]]
- ال Component Based: عندنا حاجة اسمها package manager أقدر انزل منها package/library اللي انا محتاجها في البروجكت بتاعي عن طريق ال NPM (Nuget.org Package Manager)