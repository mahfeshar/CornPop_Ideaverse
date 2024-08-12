---
up:
  - "[[HTML]]"
related: 
created: 2024-05-24
---
We can add buttons to click with `<button>
```HTML
<button>Click here</button>
```

الزرار دا في العادي مش هيعمل أي حاجة فلو عايزة يعمل submit مثلًا للفورم اللي عندي لازم أديله نوع
```html
<button type="submit" >Submit</button>
```

ممكن نعملها بالـ [[Forms HTML#submit|Submit]] عادي جدًا بس الأحسن اني أستخدم الـ Button عشان الـ Readability 
```html
<input type="submit" value="Submit" />
```

![[Pasted image 20240812143657.png]]

ممكن أخليه يعمل reset لكل الداتا اللي عندي برضو عن طريق إني أديله قيمة reset
```html
<button type="reset">Reset</button>
```