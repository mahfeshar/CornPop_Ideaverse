---
up:
  - "[[CSS]]"
related: 
created: 2024-05-24
---

- بكل بساطة اني أختار أكتر من element أعملهم نفس الحاجة سوا عشان مفضلش أكرر وعشان لو عايز أغير مفضلش أغير في كل واحد لوحده بالعكس أغير في كله مرة واحدة
```CSS
h1, h2, h3, h4, p, li {
	font-family: sans-serif;
}
```

## Descendant Selector
- فيه حاجة كمان اسمها descendant selector ودي بكل بساطة اني عندي حاجة معينة في ال p مثلًا عايز أخصصلها حجم معين، فبكتب هي فين الأول 
```CSS
footer p {
	font-size: 16px;
}

article header p {
    font-style: italic;
}
```


## Child Selector (>)
بختار الحاجات اللي هي child للعنصر بس مش أكتر انما  child بتاع ال child مش باخده 
يعني مش باخد الحفيد

```css
div > p {
	font-size: 20px;
}
```

## Adjacent Sibling Selector (+)
يعني نفذ على أول حاجة بعد الحاجة الأولى (مجاور)
```css
div + p {
	color: red;
	/* لون أول بارجراف بعد الديف */
}
```
لو لقى أي حاجة مختلفة عن ال p بعد ال div يبقا مش هتتنفذ، لازم يبقا بعده على طول

## General Sibling Selector (~)
أي حاجة جاية بعد كدا (مجاور عام)
```css
div ~ p 
{  
	background-color: yellow;
}
```
أي p هتيجي بعدها حتى لو فصل بينهم حاجة، ومش واحدة بس لا كل اللي جاي بعدها 