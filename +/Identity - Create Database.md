---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-09
---
الـ **Security Module** في التطبيقات بيتكون من عنصرين أساسيين: 

1. **Authentication** (التحقق من الهوية)
2. **Authorization** (التفويض أو التصريح)

### خطوات تنفيذ Security Module

1. **Identification/Registration** (التعريف أو التسجيل):  
   - أول خطوة هي التأكد من هوية المستخدم، ودي بتكون من خلال تسجيل المستخدم في التطبيق وإنشاء حساب خاص له. 
   - بعد كده بنقدر نعتبره مستخدم (User) داخل التطبيق بتاعنا.

2. **Login** (تسجيل الدخول):  
   - بعد ما يتم تسجيل المستخدم، بنستخدم بياناته للتحقق من هويته عند كل عملية دخول.

3. **Authorization** (التفويض):  
   - بعد عملية تسجيل الدخول، بنحدد للمستخدم الصلاحيات اللي مسموح له بها في التطبيق. بمعنى، بنحدد إيه اللي يقدر يشوفه، وإيه اللي يقدر يعمله، والحاجات اللي مش مسموح له يوصل لها.

### استخدام Microsoft Identity Package

عشان نسرع عملية تطوير الـ Security Module، بنستخدم حزمة جاهزة من مايكروسوفت اسمها **Identity**. 
الحزمة دي بتيجي مدمجة فيها مجموعة خدمات جاهزة بتساعدنا على تنفيذ المهام المطلوبة بشكل أسهل وأسرع.

#### خدمات Microsoft Identity الأساسية

1. `UserManager`:  
   - خدمة بتساعدنا على إدارة المستخدمين في التطبيق، وتوفر لنا وظائف زي:
     - إنشاء مستخدم جديد (Create)
     - تحديث بيانات المستخدم (Update)
     - حذف مستخدم (Delete)
     - البحث عن مستخدم بواسطة بياناته (Find by)

2. `SignInManager`:  
   - خدمة بتساعدنا على تنفيذ عمليات تسجيل الدخول وتوفر إمكانيات إضافية زي:
     - تسجيل الدخول (Sign in)
     - إعادة تعيين كلمة المرور (Reset Password)
     - التحقق بخطوتين (Two Factor Authentication)
     - تسجيل الدخول من مصادر خارجية (External Login)

3. `RoleManager`:  
   - خدمة لإدارة الأدوار والصلاحيات، وتتيح لنا الوظائف التالية:
     - إنشاء دور جديد (Create)
     - تحديث البيانات الخاصة بالدور (Update)
     - حذف دور (Delete)
     - تعيين مستخدم لدور معين (Assign User to Role)

### الكيانات الأساسية في Security Module

بيكون عندنا كيانين أساسيين في Security Module:

1. **User (المستخدم)**:  
   - الكلاس الخاص بالمستخدم في Microsoft Identity هو `IdentityUser`، وبيحتوي على عدة خصائص (Properties) مثل:
     - `ID`
     - `Username`
     - `NormalizedUsername`
     - `Email`
     - `PhoneNumber`
     - وخصائص أخرى لإدارة المستخدم

2. **Role (الدور)**:  
   - كلاس خاص بإدارة الأدوار والصلاحيات اللي بيمتلكها كل مستخدم. يتيح لنا تخصيص كل دور بمهام معينة أو صلاحيات داخل التطبيق.

### Customization
ممكن نعمل **تخصيص** (Customization) للـ Identity classes عشان تناسب احتياجات التطبيق بشكل أفضل. 
بنعمل كلاس خاص بينا ونسميه مثلًا `AppUser`، واللي بيورث من الكلاس الجاهز `IdentityUser`، وبكده نقدر نضيف أو نعدل الخصائص على حسب المتطلبات.

بنفس الطريقة، ممكن نعمل تخصيص لكلاس الـ Role بإنشاء كلاس خاص باسم مثلًا `AppRole`، واللي بيورث من `IdentityRole`. 
ده بيساعدنا إننا نتحكم في معلومات المستخدمين والصلاحيات بشكل أكتر مرونة، ونضيف خصائص إضافية أو نعدل في كيفية التعامل مع البيانات الخاصة بكل مستخدم أو دور.

### Installing Package
هنروح للـ Dependencies بتاع الـ Core ونضيف الباكدج دي 
`Identity.EntityFrameWorkCore`

وننزل آخر نسخة
### Entity
نعمل فولدر جوا فالـ Core زي ما قولنا جوا فولدر الـ Entities هنعمل فولدر `Identity`

![[Pasted image 20241109135745.png]]
ونعمل جواه الـ `AppUser` بتاعنا ونخليه يورث من الـ `IdentityUser` وفيه اتنين واحد Generic والتاني Non Generic
فلو استخدمنا دي دايمًا الـ ID بتاعنا هيكون String لو عايزه يبقا حاجة غير الـ String هنورث من الـ Generic
```cs
public class AppUser : IdentityUser
{
	public string DisplayName {get; set;}
	public Address Adress {get; set;}
	// هنعمل نوع اسمه ادريس
}

public class Address
{
	public int Id {get; set;}
	public string FName {get; set;}
	public string LName {get; set;}
	public string Street {get; set;}
	public string City {get; set;}
	public string Country {get; set;}

	public string AppUserId {get; set;} // Foreign Key: User
}
```

> الـ Security هنعملها Database منفصلة تمامًا
> عشان كدا لو خدت بالك هتلاقي ان الـ `Address` مورثتش من الـ `BaseEntity`
> لأن الـ `BaseEntity` هو الـ Base Class لل Entities الخاصة بالـ `StoreContext`
> وممكن تستخدمها عادي بس هيلغبط اللي هيقرأ الكود فبلاش

مش هنقدر نعمل `BaseEntity` لل Security عشان الـ Id في الـ Address نوعه Int انما في الـ User بيبقا String
وفي الحقيقة مش محتاجه

وبرضو فيه First name و Last name عشان ممكن حد تاني يستقبل الـ Order

وبعدين نظبط العلاقة بين الـ User والـ Address لأنها 1:1 فهنحط الـ Key بتاع الـ user في الـ Address

### DbContext
هنعمل DbContext للـ Security زي ما اتفقنا 
هنعمل في نفس الـ **Repository Layer** نفس التقسيمة عادي بس للـ Security 

![[Pasted image 20241109143026.png]]
ولسا الـ Migrations ونحط كمان الـ DbContext Class
بس الفرق هنا هيورث من الـ `IdentityDbContext` مش العادية عشان يورث الـ 7 DbSet
```cs
public class AppIdenetityDbContext : IdentityDbContext
{
	
}
```
عندنا 3 نسخ من الـ `IdentityDbContext`:
- العادية ودي بتاخد الـ Identit