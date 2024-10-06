---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-13
---

انك بتخلي الكود ي survive ضد أي حاجة ممكن تحصل في ال runtime سواء expected or unexpected
وهيبقا عيب في حقك كمبرمج ان الكود بتاعك يرمي exception في وش ال user

بكل بساطة المفروض أعمل check قبل ما ال exception دا يحصل وأتوقع انه هيحصل واشوفله حل
```cs
if (Y != null)
	X = (int) Y;
else
	X = 0;
```
فكدا حليت المشكلة ببساطة ان البرنامج مش هيرمي exception
ممكن بدل الكود اللي فوق دا أستخدم شوية properties جوا ال nullable types
```cs
if (Y.HasValue) // bool
	X = Y.Value;
else
	X = 0;

X = Y.HasValue ? Y.Value : 0;

X = Y ?? 0; // Same as before, with nullable types
```