
# Session 3
Chunks -> link it with each other
لو كل الداتا ورا بعض دا بيبقا حلو لأن بيرتريف كويس، انما لو بعيد عن بعض بيعمل لود لكل شانك 
بتعمل ديفراجمنتيشن عشان يظبط الدنيا ويرتب الهارد تاني

---
Task: نعرف الريكوردات والكلاس
هل الكلاس immutable ولو لا ازاي نخليه كدا
الريكورد نفس السؤال

---
## Object Oriented

- أشهر paradigm 
New Item -> class

we will use global.

كل namespace بيتحول ل assembly في الميموري وبعدها بتتحول لمجموعة من الأوامر وبعدين dll ويبدأ ينفذها

indentation -> الإزاحة اللي روحتها 

بعمل semicolon جنب ال namespace بيقلل ال indentation 

لو زودت كمان namespace معنى كدا ان فيه dll تاني هيطلع معايا

Entry assembly: اللي ببدأ بيها وبتبقا المين ونقدر نعدلها بعد كدا
Executing assembly: اللي شغاله دلوقتي

لحد السباكة

---
ال class القالب بتاع السباكة اللي عشان أعمل زي تيمبلت أعمل منه أنواع تانية، وبيطلع زي النسخة الأصلية بالظبط


عملية استنساخ أو توليد اوبجكت اسمها instantiation 

---
debug - release 

---
وانا بعرف الكلاس ممكن اعرف namespace كانت متعرفة قبل كدا عشان بقوله قبل كدا 

---
بعمل شغل حلو في كلاس واحدة بس والباقي يورث منه

---
بستخدم ال override بكلمة override

مش هيورث ال internal لو مش موجودين فنفس ال namespace ومش بيورث ال protected

---
field - property


abstract class - struct - class - record
الفرق بين abstract class - seald class 
record class

class mutable or imm and how to change
recode
tuple

---
Collections and generics

---
How to make editor know after new;

# Session 4
## WebAPI
الراجل بتاع الفرونت بيبقا عايز يتأكد ويهندل الداتا عشان اليوزر يستخدمها كويس بس المشكلة إنه ميعرفش باك وميعرفش يتعامل مع السيرفرات وكدا 
فعشان كدا بنعمل طبقة وسيطة واللي بيعملها شخص فاهم فالباك أو في السيرفر سايد بحيث ياخد الداتا وبيربطها مع URL معين عشان ال front يتعامل معاها
هو الفرونت مثلًا بيعمل شوية زراير أو buttons وال API بتطبق مبدأ ال interfaces انه بيخلي حاجة بتنادي على حاجة وتستخدمها من غير ما يبقوا لامسين بعض، زي السنترال وبيبقا له Single responsibility
ممكن يبقا عندي السيرفر فيه بلاتفورم (لينكس) وبلاتفورم عليه البراوزر - ممكن مبيبقوش بيفهموا بعض عشان كدا عملنا الوسيط دا (Cross platform)

API: Application programmable interface
المبرمج هيعملها وينشرها على Fully qualified domain name بيبقا معرف بالكامل زي facebook.com
ودا اللي هيديني ال API
محتاج حاجة كمان اسمها ال Route، يعني كل method تبقا في طريق
## URI vs URL
URI = Tells you in which hotel you should go to sleep.
URL = Tells you in which room in what hotel you should go to sleep.
So URL is a lot more specific, it points to a final destination. The thing you want. While URI is something strange.

---
URI: Uniform Resource Identifier (URI) is a string of characters used to identify a name or a resource on the Internet. Such identification enables interaction with representations of the resource over a network (typically the World Wide Web) using specific protocols

URL: In computing, a Uniform Resource Locator (URL) is a subset of the Uniform Resource Identifier (URI) that specifies where an identified resource is available and the mechanism for retrieving it.
بنحتاج ال Protocol 

**Example**

To identify a specific resource and how to access it - in all completeness

```
URI: mysql://localhost@databasename:password
```

The URL shows you where you can find the database on the internet and which protocol you should use.

```
URL: mysql://localhost
```

## Build and publish
لما بتيجي تعمل build للsolution قولنا انك ممكن تعمل الحوار دا release او debug
ممكن تعمله publish وهيطلعلك exe فايل عالتشغيل

---
لو عايز حاجة cross platform هنستخدم class library بدل console application وهيشتغل مع كله والخرج بتاعه هيبقا dll فايل، بس الفايل دا بيحتاج اللي يشغله من الأخر
هنستخدم nssm.exe عشان نعمل windows service

## Web API
Configure for HTTPS
Enable container support -> docker file
Enable OpenAPI support
use controllers

باقي الكلام عن الـ API في السيشن 7
زي الـ return status بتاعنا 

---
## Global using
اني اعمل فايل جديد واسميه `GlobalUsings.cs` وابدأ احط فيه كل ال libraries اللي هستخدمها في كل البروجكت 
بس لازم أحدد انه يبقا global
```cs
golbal using Microsoft.AspNetCore.Mvc;
```
دا بيبقا حلو إنه بيحمل ال library مرة واحدة 
بتخلي ال compiler لما بيعمل precompile وبيجهزها قبل ما يعمل Build ودا بيعملها في A hit of time compilation ودا بيسرع ال Output بتاعنا


# Session 7 - windows Forms app

بنتارجت الـ Windows Desktop Platforms

Windows Form: من أقدم السوليشنز

### Properties 
- نقدر نتحكم في كل الـ Properties ودي بتتكا F4 أو من الـ View بتظهرها 
- تقدر تغير الشكل اللي بيظهر فيه وكل حاجة تقريبًا واسمه وكمان لون الـ BG 

![[Pasted image 20240731135845.png]]

### Toolbox
- عشان تقدر تضيف بقا الزراير وكدا
- هتلاقيها في View
- بتاخد الحاجات Drag & Drop بكل بسيطة وتقدر تغير شكلها واسمها وكدا من الـProperties

![[Pasted image 20240731140044.png]]

## Add functionality for every thing
- لما بتتكا double click على أي زرار بتلاقي الكود ظهرلك له عشان تضيفله يعمل ايه بالظبط
- بتاخد داتا من اليوزر وتستخدمه فالبرنامج بتاعك انك تخزنها وتعمل parsing وكل حاجة
- لو عايز أظهر حاجة للـ User فدا عن طريق الـ Labels وخليه فاضي

## Errors 
- تقدر تعمل [[Cs Handle Exception]] وتظهر الـ Error في حاجة من اتنين:
	- اما Label وتبقا فاضية
	- أو انك تستخدم Message

```cs
try
{
	int studentAgeTest = int.Parse(StudentAge.Text);
}
catch(Exception exception)
{
	// Error.Text = exception.Message; // Label Name
	MessageBox.Show(exception.Message, "Error"); // Message Box
	return;
}


// Another way
bool isAgeValid = int.TryParse(StudentAge.Text, out int studentAge)

// 18 -> Parse -> studentAge
// usAgeValid -> Try -> True
```