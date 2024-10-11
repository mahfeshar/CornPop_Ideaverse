---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-11
---
- هو كلاس أقدر أقسم الكود بتاعه على أكتر من فايل
- يعتبر تنظيم للشغل مش أكتر
نشرحها بمثال:
لو تفتكر في الـ [[Code-first or Database-First]] كنا قولنا إننا ممكن نعمل الـ Database الأول ومن خلالها بنستخدم ORM يحولي الـ Table لـ Class

![[Pasted image 20241011063204.png]]
- في المثال دا أنا عملت الجدول فالأول بـ ID و Name و Age فأنت لما هتعمل Mapping هيتحول للأخضر اللي عاليمين
- حبيت أزود Method على الـ Class عشان أستخدمها وهي Print
- بس جيت مع الوقت وحبيت أغير حاجة في الجدول أو أزود حاجة فبتضطر إنك تعمل Mapping تاني ويعيد تكوين الـ Class فبالتالي هيمسح أي حاجة غير العماويد اللي في الجدول
- عشان كدا الـ Entity Framework ذكي لأنه بيعملي الـ Class اللي معموله Mapping بنوع Partial فأنت لو حبيت تزود حاجة أو تنقص حاجة بتزودها في فايل تاني ومهما حصل مش بتأثر على دا
  يعتبر التكملة بتاعته من الأخر
```cs
partial class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int? Age { get; set; }
}
```
دا الـ Class العادي اللي بيطلع من عملية الـ Mapping
عشان أشتغل أنا بعمل file class تاني بإسم `Employee.Developer.cs` وممكن تغير كلمة ديفولوبر لأي اسم
```cs
partial class Employee
{
    public void Print()
    {
        Console.WriteLine("Hello World");
    }
}
```
أي واحدة منهم لو ورثت بتسمع في التانية ومش لازم تكتب إنها وارثة منها 
ولو عايز تكتب عشان انت تعرف وأنت شغال انت وارث من إيه عادي تكتب في الإتنين