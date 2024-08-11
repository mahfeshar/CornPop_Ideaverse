---
up:
  - "[[Data Structure and Algorithms MOC]]"
related: 
created: 2024-08-08
---

- الـ [[Sliding Window]] حالة خاصة منها
## Problem
**Check if an array is a palindrome**
- ممكن حل إنك تبني Reversed List من الأصلية وتقارن كل عنصر باللي يقابله بس دا هياخد ميموري وتايم
- الحل بالـ Two Pointers مش هياخد Memory وهياخد وقت أقل
	- هنحط Pointer فاليمين وواحد في الشمال ونقارن الإتنين ببعض
	- لو متساويين هنزود اللي عالشمال وننقص اللي عاليمين
	- لو مختلفين ترجع False

![[Pasted image 20240807191034.png]]

## Problem 2
**Given a sorted input array, return the two indices of two elements which sum up to the target value. Assume there's exactly one solution**

- الحل الـ Brute Force إننا نعمل إتنين Pointer ونعدي على كل عنصرين ونجمعهم ببعض بس دي هتاخد وقت طويل أوي
- الحل بالـ Two pointers:
	- هنعمل Pointer على أكبر رقم عاليمين ونقارنه بأصغر رقم عالشمال ببوينتر برضو
	- لو أكبر دا معناه ان مفيش اي عنصر فالـ Array تقدر تجمعه على أكبر رقم دا ويطلعلك الـ Target
	- لو أصغر يبقا كدا الرقم اللي عالشمال مستحيل ييجي معانا تاني
	  لأن مستحيل لو صغرنا الرقم اللي عاليمين كمان ييجي مع الرقم الأصغر مع الشمال فهنزود واحد شمال

![[Pasted image 20240807192017.png]]
- ودي هتبقا **O(n)**