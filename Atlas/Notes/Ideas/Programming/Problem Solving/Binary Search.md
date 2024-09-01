---
up:
  - "[[+/Problem Solving|Problem Solving]]"
related: 
created: 2024-09-01
---

## Binary Search

**Binary Search**: search in a sorted array by repeatedly dividing the search **interval in half**.
مش بتنفع غير لما الفانكشن monotonic (ليها تون واحد) إما بتطلع بس أو بتنزل بس
### How
- Begin with an interval covering the whole array.
- If the value of the search key is **less than the item in the middle** of the interval, **narrow the interval to the lower half**.
- Otherwise narrow it **to the upper half**.
- Repeatedly check until the value is found or the interval is empty.

---

- Given a array of _**N**_ elements, write a program to search a given element _**x**_ in array
- A simple approach is to do linear search. The time complexity of above algorithm **is O(n)**. Another approach to perform the same task is using Binary Search, and it’s time complexity **is O(log2(n))**

![Binary Search](https://cdn-images-1.medium.com/max/1200/1*EYkSkQaoduFBhpCVx7nyEA.gif)

---
- لازم الـ Array يبقا معمولها Sort
- هنعمل two pointers واحد في أول الـ Array والتاني فالأخر ونسميهم أي حاجة مثلًا a, b
- هنروح نشوف الرقم اللي فالنص ونشوف هل هو أصغر من القيمة اللي عايزها ولا أكبر ولا يساوي
- لو أصغر يبقا هنقل الـ pointer اللي فالأول (عالشمال) ونحطه فالنص لأنه مستحيل يبقا فالشمال
- لو أكبر هننقل الـ Pointer اللي فالأخر (عاليمين) ونحطه فالنص
- لو يساوي يبقا كدا خلاص
- لو الرقم مش موجود فنوقف
## Lower and Upper Bound
لو مش عايز أجيب الرقم نفسه بس عايز أجيب الرقم الأكبر منه أو اللي قده
هنشرح على الـ Lower Bound

![[Pasted image 20240901175653.png]]
مثلًا في المثال دا عايز أجيب أول رقم أكبر من أو يساوي الـ 18
فأنا هنا هيبقا عندي إما الرقم دا أصغر منه (Invalid) أو أكبر منه أو يساويه (Valid)

فكدا معنديش غير احتمالين يعني لو طبقت نفس اللي فوق:
- لقيت الرقم أصغر من الرقم المطلوب يبقا كدا كل اللي قبله Invalid فممكن أرميه وحتى نفسه مينفعش
- لقيت الرقم أكبر من الرقم المطلوب يبقا كل اللي بعده برضو مش عايزه لأن الرقم اللي انا عليه دا ممكن يبقا هو الـ Upper أو الـ Upper أصغر منه  (هو نفسه ينفع)

نكمل المثال هنحط البوينتر في النص عند الـ 17 ونشوف ينفع ولا لا فهو أقل فمينفعش فأنقل الـ Pointer بعده

![[Pasted image 20240901180020.png]]
وهكذا

### Edge case
- لو كل الأرقام أصغر منها ومفيش ولا رقم ينفع فعندي حلين:
	- إما ان الاتنين بوينترز يبقوا على بعض وبرضو إن الرقم Invalid بعمل check وبقول ان مفيش
	- إني أعمل فالأخر رقم وهمي مش عندي اسمه inf ولو وصلتله يبقا كدا مفيش ولا رقم ينفع

![[Pasted image 20240901180848.png]]