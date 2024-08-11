---
up:
  - "[[Data Structure and Algorithms MOC]]"
related: 
created: 2024-07-06
Link: https://www.youtube.com/watch?v=XX7DeDqqrV8
---

- لو فيه Algorithm عملته وهو كويس أوي من كل حاجة 
  بس من وقت للتاني بيحصل عملية بتاخد Time عالي أو بتعمل Expensive cost 
  فمينفعش ألغي ال Algorithm وأقول انه وحش بسبب كدا 
- ممكن تفكر فيه انه Average time

We have three common amortization arguments:
1. The aggregate method
2. The accounting method
3. The potential method

## Aggregate method
- عايز أحسن ال Total cost بتاعي

$$
Cost(N.operations) / n = (Cost(normal.operations) + Cost(Expensive.operations)) / n
$$
![[Pasted image 20240706160119.png]]

### Example: Dynamic Array
- في ال hash table عشان أحدد مساحة ال Table بتاعي فعندي Trade-off بين ال Space and Time
	- يعني لو عملنا Table كبير أوي ال Search time هيبقا أسرع بس المساحة هتبقا مش كويسة
	- من هنا جت فكرة ال Dynamic Array
الخطوات أول ما ال Array تتملى:
1. أعمل واحدة جديدة في ال memory وتبقا مساحتها أكبر مرتين من اللي فاتت (2 * n)
2. حط القيم من ال Array القديمة للجديدة
3. امسح القديمة أو اعملها Free memory

---
لو جينا نحسب ال Time Complexity بالطرق العادية
- The worst case cost of one insertion is ==O(n)==
- The worst case cost of n insertion is n * O(n) = ==O($n^2$)==
بس هل دا صحيح ؟

---
![[Pasted image 20240706161651.png]]
- كل عملية هتكلف C وقت 1 بس دا لو بنضيف عادي O(1)
- انما ال Expensive operations اللي هي لما باجي أزود حجم ال Array الضعف اللي هي تحت خالص

![[Pasted image 20240706161844.png]]
- هنجمع ال Cost بتاع الطبيعيين ($n$) وكمان ال Expensive اللي هيطلعوا في الآخر ($2 * n$)
- لما نستخدم القانون بتاعنا اللي فوق هنلاقي انها $O(n)/n$ 
### Why $2  * n$ ?
![[Pasted image 20240706164431.png]]
- آخر Term دايمًا بيبقا أكبر من كل اللي قبله 
  يعني فوق لو اعتبرنا ان 8 آخر حد فهو أكبر من $1 + 2 + 4 = 7$ 
- عشان كدا احنا بنعمل **Doubling** مش بنضرب في 3 مثلًا
- عشان أعمل Array ب size يساوي 8 فهي هتاخد 15 عملية والرقم دا دايمًا هيبقا أقل من أو يساوي $2*n$ 