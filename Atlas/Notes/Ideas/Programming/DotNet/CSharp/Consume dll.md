---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-23
---

## First Method
- أول طريقة إننا نكتب class جوا الـ Library دي 
- بعدين Alt + Enter وتعمل Install ليها وتضيفها

## Second Method
- تعمل كليك يمين على البروجكت
- اختار Add -> Reference (COM)
- وتختار الـ `dll`
## Third Method
- تدخل هنا [NuGet Gallery | Packages](https://www.nuget.org/packages) وإني أقدر أرفع الفايل هنا وتستخدمه كـ CDN
- تدور على الـ Package اللي انت عايزها مثلًا `System.management`
- تعملها Install
- فيه أكتر من طريقة:
	- بالـ .NET CLI أو بالـ Package Manager وفيه طرق تانية كتير
	- ممكن من الـ VS نفسه تختار View وبعدين Package Manager Console 
	- أحسن طريقة: اضغط على الـ Project رايت كليك، وبعدها Manage NuGet

> [!todo] Important
> لو ضغطت على الـ Project هتلاقي كل الـ Packages and Libraries اللي موجودين فيها وتقدر تضيف جديد فيها Reference بس الطريقة دي مش مسموح بيها

لو عايز تشوف الكلام دا هتروح على الـ Dependencies وتروح على الـ Analyzer أو في الـ Packages