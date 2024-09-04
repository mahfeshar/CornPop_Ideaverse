---
up:
  - "[[Problem Solving|Problem Solving]]"
related: 
created: 2024-09-01
---

![Binary Search](https://cdn-images-1.medium.com/max/1200/1*EYkSkQaoduFBhpCVx7nyEA.gif)
## Binary Search
- **Binary Search**: search in a sorted array by repeatedly dividing the search **interval in half**.
- مش بتنفع غير لما الفانكشن monotonic (ليها تون واحد) إما بتطلع بس أو بتنزل بس
- بتشتغل على الحاجات الـ Sorted بس
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
  We consider the segment $[l,r]=[1,9]$, the middle element is at the position $\frac{l+r}{2}=5$.

![[Pasted image 20240904081950.png]]
- نبص على النص الجديد وهكذا لحد ما نوصل للعنصر اللي بندور عليه.
  We consider the segment $[l,r]=[1,4]$, the middle element is at the position $\frac{l+r}{2} = 3$.

![[Pasted image 20240904082544.png]]
الطريقة دي أسرع بكتير من البحث العادي لأنها بتقلل حجم المصفوفة اللي بندور فيها للنص في كل خطوة، وبالتالي بتاخد وقت **O(log n)**.
### How
- Begin with an interval covering the whole array.
- If the value of the search key is **less than the item in the middle** of the interval, **narrow the interval to the lower half**.
- Otherwise narrow it **to the upper half**.
- Repeatedly check until the value is found or the interval is empty.

---

- Given a array of _**N**_ elements, write a program to search a given element _**x**_ in array
- A simple approach is to do linear search. The time complexity of above algorithm **is $O(n)$**. Another approach to perform the same task is using Binary Search, and it’s time complexity **is $O(log_2(n))$**

---
- لازم الـ Array يبقا معمولها Sort
- هنعمل two pointers واحد في أول الـ Array والتاني فالأخر ونسميهم أي حاجة مثلًا a, b
- هنروح نشوف الرقم اللي فالنص ونشوف هل هو أصغر من القيمة اللي عايزها ولا أكبر ولا يساوي
- لو أصغر يبقا هنقل الـ pointer اللي فالأول (عالشمال) ونحطه فالنص لأنه مستحيل يبقا فالشمال
- لو أكبر هننقل الـ Pointer اللي فالأخر (عاليمين) ونحطه فالنص
- لو يساوي يبقا كدا خلاص
- لو الرقم مش موجود فنوقف
### البحث عن أقرب عنصر:

لو عايزين نلاقي أقرب عنصر لعدد معين (مش شرط نلاقي العدد نفسه)، ممكن نستخدم نفس فكرة Binary Search
If we needed to find an element exactly equal to $x$, then we could use a [[Hashing|hash table]]. But if there is no $x$ element in the array, then the hash table will simply indicate this. In this case, we need to solve the following two tasks:
- Find the maximum element not greater than $x$ (closest to $x$ on the left)
- Find the minimum element not less than $x$ (closest to $x$ on the right)

### مثال
Consider a binary search algorithm for solving the first problem (**maximum element not greater than $x$**)

Let's take an example $a=[3,5,10,11,13,18,25,27,31]$, $x=20$.

![[Pasted image 20240904083335.png]]
Since $x=20$ is greater than $a_m=13$, then $l=m$

![[Pasted image 20240904083616.png]]
Since $x=20$ is less than $a_m=25$, then $r=m$

![[Pasted image 20240904083658.png]]

![[Pasted image 20240904083705.png]]

Since the invariant is satisfied, then $a_l≤x$, and $a_r>x$, in this case, $l$ is the maximum of such indices, and $r$ is the minimum.

What happens in special cases?

- If all items are greater than x, then $l=−1$.
- If all items are less than x, then $r=n$.

But since we set these elements equal to $±∞$, the correctness the algorithm will not be violated.

كل دا اللي هو [[Lower and Upper Bound]]

## Code
### c++
```cpp
int binarySearch(vector<int> arr, int target) {
    int L = 0, R = arr.size();

    while (L <= R) {
        int mid = (L + R) / 2;

        if (target > arr[mid])
            L = mid + 1;
        else if (target < arr[mid])
            R = mid - 1;
        else
            return mid;
    }
    return -1;
}
```
### Python
```py
arr = [1, 3, 3, 4, 5, 6, 7, 8]

# Python implementation of Binary Search
def binarySearch(arr, target):
    L, R = 0, len(arr) - 1

    while L <= R:
        mid = (L + R) // 2

        if target > arr[mid]:
            L = mid + 1
        elif target < arr[mid]:
            R = mid - 1
        else:
            return mid
    return -1
```
## Problems
