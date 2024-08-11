---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-25
---
### Inheritance
- هي بكل بساطة الوراثة ان بعض ال elements بتورث صفاتها وخصائصها ل elements تانية
- يعني مثلًا لو اديت شوية خصائص لل body وانت عارف ان دا ال parent لكل العناصر الباقية فكدا أي عنصر هيورث الخصائص دي
- بس افتكر حوار ال priority فلو فيه خاصية غيرتها في مكان تاني أعلى أولوية هتعتبر انك معملتهاش بس هي في الحقيقة بتتعمل
- بس خد بالك انها مش بتورث كل الخصائص يعني هي مش بتطبق كل ال styles لكل الخصائص الأصغر منها أو اللي جواها يعني لو جيت مثلًا
```css
body {
	/*Will be inherted*/
	color: #444;
	font-family: sans-serif;

	/*Will be applied to the top of the page*/
	border-top: 10px solid #1098ad;
}
```
![[Pasted image 20240307083207.png]]

### Universal Selector
هو بكل بساطة حاجة بتلم كله وبتورث لكل اللي في الصفحة
```css
* {
	color: #444;
	font-fanily: sans-serif;
	border-top: 10px solid #1098ad;
}
```
الفرق بينها وبين ال body ان دي حرفيًا بتنفذ أي استايل على كله يعني في المثال اللي فوق هيبقا كل عنصر فوقه border


