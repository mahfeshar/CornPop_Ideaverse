---
up:
  - "[[CSS]]"
related: 
created: 2024-05-24
---

### Inline
- ممكن تكتب كود ال CSS جوا ال elements بتاع ال HTML 
- بس محدش ينصح بالطريقة دي لأن غلط انك تخلي الاتنين في نفس اللاين 
```HTML
<h1 style="color:blue">This is head</h1>
```

### Internal
- ممكن تكتب الكود في نفس فايل ال HTML في ال head بعنصر style وتكتب جواها كل كود ال CSS 
- بس دي مشكلتها ان لو الكود كبير هيعمل مشاكل انه هيكبر حجم الفايل
```HTML
<head>
	<style>
		h1 {
			color: blue;
		}
	</style>
</head>
```

### External
- دي أحسن طريقة انك تكتب الكود في فايل تاني ودي أحسن طريقة
```CSS
style.css
h1 {
	color: blue;
}
```
- هنا ممكن تسمي الفايل أي حاجة على عكس ال HTML أول فايل بيبقا اسمه index
- بس لازم تربط الفايلين ببعض وهنا هنستخدم attribute جديد
#### Link
- بنستخدمه جوا *head* وبيستخدم عشان نربط فايل ال CSS بفايل ال HTML
```HTML
<head>
	<link href="style.css" rel="stylesheet" />
</head>
```
