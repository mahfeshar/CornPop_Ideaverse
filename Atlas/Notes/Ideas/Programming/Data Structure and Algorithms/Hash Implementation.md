---
up:
  - "[[Data Structure and Algorithms MOC]]"
related:
  - "[[Hashing]]"
  - "[[Hash Usage]]"
created: 2024-07-23
---

- مش مشهورة أوي في الإنترفيوهات
- هنستخدم [[Array]] عادية خالص
- طبعًا الـ Array مش هتبقا فاضية فالأول وهيبقا ليها Size معين والقيم بتاعته Null

![[Pasted image 20240723144609.png]]

- نفترض إن الـ Size بتاعي ب 2
- لو خدت بالك الـ Array ليها Index عادي والقيمة بتاعها بتنقسم لحاجتين Key, Value بتوع الـ Map
- اللي يهمني دلوقتي هو الـ **Key**، لأن هو اللي هقدر من خلاله أوصل للـ Value
- الخطوة كالآتي:
	- لما أجي أضيف Key, Value جديد للـ Map هيحول الـ Key لرقم Int عشان يعرفه بالـ Index
	- نفترض كلمة Alice هتبقا بتساوي 25 (بيحول كل حرف لرقم ويجمعهم)، فالـ Index المفروض يبقا 25 بس أنا الـ size بتاعي ب2 بس
	- نحلها بإننا ناخد الـ Mod بتاع الرقم بالنسبة للـ size بتاع الـ array، يعني الـ 5%2 = 1
	- يعني Alice هتبقا بـ 25 وبعدين Mod هتبقا بـ 1 فهتتخزن في الـ index الأول
- لو حبيت أعمل get للكلمة دي فنقدر نجيبها في **O(1)**، لأن بيحصل عكس العملية دي

## Hashing Collision 
- أكيد جه في دماغك دلوقتي طب لو اتنين Keys بقا ليهم نفس الـ Index
- دي بالظبط مشكلة موجودة وتقدر تقللها بس برضو هتفضل موجودة مش هتخلص

### Doubling the size
- لو لقيت الـ Array بدأت تتملى (نصها مليان) فأنت المفروض تعملها double الحجم زي فكرة الـ [[Array#Dynamic Arrays|Dynamic Array]] بالظبط
- يعني المثال اللي فوق دي لما حطينا Alice في الـ Array بقا نصها مليان فبالتالي هنبدأ نعمل array جديدة حجمها الضعف
- بس بعد كدا كل العناصر اللي موجودة في القديمة هتعملها rehashing والمرادي هتاخد الـ Mod بالنسبة للـ Array الجديدة (ممكن يطلع مكان جديد وممكن يبقا نفس المكان، المهم تتحط فالمكان الصح)
- طيب أنا كدا حليت المشكلة؟ أكيد لأ


> [!globe] The best
> الأحسن إن الـ Size بتاع الـ Array يبقا Prime Number لأن دا هيقلل الـ Collision شوية
### Still Collision 
في الحالة دي عندي حل من إتنين وهما:
1. **Open Addressing:**
    - **Linear Probing:** Search for an empty slot sequentially
    - **Quadratic Probing:** Search for an empty slot using a quadratic function
2. **Closed Addressing:**
    - **Chaining:** Store colliding keys in a linked list or binary search tree at each index
    - **Cuckoo Hashing:** Use multiple hash functions to distribute keys

- بكل بساطة الحل Closed دا اللي هو عملية الـ Chaining دي بكل بساطة إن كل Index بدل ما بياخد عنصر واحد ياخد Linked List كاملة
	- مشكلتها انها بتاخد من الـ Memory كتير وكمان طريقة الـ Handling هتبقا صعبة لأن انت جوا كل Index المفروض تظبط Pointers وحاجات من دي 
- الحل التاني اللي هو الـ Open ودا بكل بساطة إن لو لقيت حاجة في الـ Index بتاعي أزود واحد على الرقم بعد ما عملتله Mod 
  فبالتالي هينزل على اللي بعدها، ولما أجي ادور عليها لو ملقتوش في مكانه انزل تحت واحد 
  وهكذا لحد ما تقابل مكان فاضي ولو لقيت مكان فاضي يبقا كدا وقف واللي بتدور عليه مش موجود

الموضوع أكبر من كدا وممكن تدور فيه بس دي الخلاصة

## Implementation 
- الكود مش مهم أوي بس أعرف الحاجات الأساسية المهمة اللي فيه
### Python
```python
class Pair:
	# This class because every Index will have key and value 
	# To store it easy
	def __init_(self, key, val):
		self.key = key
		self.val = val

class HashMap:
	def __init__(self):
		self.size = 0
		self.capacity = 2
		# Real Map: Array with capacity 2
		self.map = [None, None]

	# Key -> Hash code
	def hash(self, key):
		index = 0
		for c in key:
			index += ord(c)
		# Mod
		return index % self.capacity

	def get(self, key):
        index = self.hash(key)
        
        while self.map[index] != None:
            if self.map[index].key == key:
                return self.map[index].val
            index += 1
            index = index % self.capacity
        return None

    def put(self, key, val):
        index = self.hash(key)

        while True:
            if self.map[index] == None:
                self.map[index] = Pair(key, val)
                self.size += 1
                if self.size >= self.capacity // 2:
                    self.rehash()
                return
            elif self.map[index].key == key:
                self.map[index].val = val
                return
            
            index += 1
            index = index % self.capacity
    
    def remove(self, key):
        if not self.get(key):
            return
        
        index = self.hash(key)
        while True:
            if self.map[index].key == key:
        # Removing an element using open-addressing actually causes a bug,
        # because we may create a hole in the list, and our get() may 
        # stop searching early when it reaches this hole.
                self.map[index] = None
                self.size -= 1
                return
            index += 1
            index = index % self.capacity

    def rehash(self):
        self.capacity = 2 * self.capacity
        newMap = []
        for i in range(self.capacity):
            newMap.append(None)

        oldMap = self.map
        self.map = newMap
        self.size = 0
        for pair in oldMap:
            if pair:
                self.put(pair.key, pair.val)
    
    def print(self):
        for pair in self.map:
            if pair:
                print(pair.key, pair.val)
```