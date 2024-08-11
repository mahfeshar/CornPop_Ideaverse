---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-06-08
---
زي ال CSS لو عايز أربط فايل JavaScript ممكن أكتبه Internal أو External
[[JavaScript MOC]]
## Internal
انك تكتبه في نفس الفايل ال HTML
مش بتبقا أحسن طريقة عشان كله بيبقا داخل في بعضه
```html
<script>
	alert("Welcome In HTML");
</script>
```

## External
انك تكتب الكود بتاعك في فايل برا وبعدين تربطه بالفايل الحالي
```html
<script src="script.js"></script>
```
