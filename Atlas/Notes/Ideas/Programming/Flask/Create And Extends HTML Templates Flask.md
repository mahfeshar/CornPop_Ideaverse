---
up:
  - "[[Flask]]"
related: 
created: 2024-07-25
---

- هنعمل Base HTML file وبعدين نعملها Extend والصفحات التانية تاخد منها 
## Why
- نفترض ان عندي 1000 ملف HTML وجه العميل عايز يغير اسم الـ CSS file أو يضيف واحد جديد
- الحل إنك تعدل على الـ 1000 كلهم بس دا مش حل كويس
- الحل يبقا عندي Base file كل الفايلات التانية بتعتمد عليه فالحاجات اللي بتكرر والجزء اللي بيتغير زي الـ Body يتغير عادي 

## How
- هتعمل صفحة HTML عادية خالص وتسميها أي اسم وليكن base
- تكتب الكود بتاعك بس جزء الـ Body تعرفه ان دا هيتغير
```html
<body>
 {% body block %}
 {% endblock %}
</body>
```
- بعدين تروح بقا على صفحة انت عايزها تاخد الكود من دي وتعرفه انك هتعمل extend من الملف base
- خد بالك الصفحة دي لازم تبقا في فولدر سميه templates مثلًا 
```html
{% extends 'base.html' %}
{% body block %}
<h1>HTML code</h1>
We will write just this code, no head, no namespaces 
{% endblock %}
```