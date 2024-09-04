---
up:
  - "[[Problem Solving|Problem Solving]]"
related: 
created: 2024-09-01
---
## Binary Search

**Binary Search**: search in a sorted array by repeatedly dividing the search **interval in half**.
مش بتنفع غير لما الفانكشن monotonic (ليها تون واحد) إما بتطلع بس أو بتنزل بس
بتشتغل على الحاجات الـ Sorted بس
### الفكرة الأساسية:
عندنا مصفوفة مرتبة بشكل تصاعدي، وعايزين نلاقي مكان عنصر معين فيها بشكل سريع. 
لو عملنا البحث ب**الطريقة العادية** اللي هي نمشي من أول المصفوفة لحد آخرها، هنحتاج وقت **O(n)**، وده مش فعال لو المصفوفة كبيرة.

### إزاي نخلي البحث أسرع؟
بما إن المصفوفة **مرتبة**، نقدر نستفيد من الترتيب ده. هنبدأ نبص على العنصر اللي في النص:
- لو العنصر ده **أكبر** من اللي إحنا بندور عليه، نقطع النصف اللي على اليمين.
- لو **أصغر**، نقطع النصف اللي على الشمال.

نفضل نكرر العملية دي لحد ما نوصل لعنصر واحد، اللي إما يكون هو اللي بندور عليه أو مش هو.

### مثال:
لو عندنا مصفوفة `[3, 5, 8, 13, 18, 19, 21, 27, 32]` وعايزين ندور على العنصر `13`:
![[Pasted image 20240904081840.png]]

- في الأول نبص على العنصر اللي في النص (العنصر الخامس 18)، وبما إن 18 أكبر من 13، نقطع الجزء اليمين.
  We consider the segment $[l,r]=[1,9]$, the middle element is at the position $(l+r) / 2=5$.

![[Pasted image 20240904081950.png]]
- نبص على النص الجديد وهكذا لحد ما نوصل للعنصر اللي بندور عليه.

الطريقة دي أسرع بكتير من البحث العادي لأنها بتقلل حجم المصفوفة اللي بندور فيها للنص في كل خطوة، وبالتالي بتاخد وقت O(log n).
### How
- Begin with an interval covering the whole array.
- If the value of the search key is **less than the item in the middle** of the interval, **narrow the interval to the lower half**.
- Otherwise narrow it **to the upper half**.
- Repeatedly check until the value is found or the interval is empty.

---

- Given a array of _**N**_ elements, write a program to search a given element _**x**_ in array
- A simple approach is to do linear search. The time complexity of above algorithm **is $O(n)$**. Another approach to perform the same task is using Binary Search, and it’s time complexity **is $O(log_2(n))$**

![Binary Search](https://cdn-images-1.medium.com/max/1200/1*EYkSkQaoduFBhpCVx7nyEA.gif)

---
- لازم الـ Array يبقا معمولها Sort
- هنعمل two pointers واحد في أول الـ Array والتاني فالأخر ونسميهم أي حاجة مثلًا a, b
- هنروح نشوف الرقم اللي فالنص ونشوف هل هو أصغر من القيمة اللي عايزها ولا أكبر ولا يساوي
- لو أصغر يبقا هنقل الـ pointer اللي فالأول (عالشمال) ونحطه فالنص لأنه مستحيل يبقا فالشمال
- لو أكبر هننقل الـ Pointer اللي فالأخر (عاليمين) ونحطه فالنص
- لو يساوي يبقا كدا خلاص
- لو الرقم مش موجود فنوقف

## Code

## Problems
