---
up:
  - "[[Data Structure and Algorithms MOC]]"
related: 
created: 2024-07-05
---

Array is a continues block of data and stored in a same way in RAM
## How we can store array in RAM
- Single value(int) from array will be stored at 8 bytes (32 bits) 
  so 1 will be 00..1 (zeros then just 1)
- RAM have two components (Value, Address)

![[Pasted image 20240503122014.png]]
# Static Arrays
## Reading Data from an Array
- __It will take O(1)__
- When you want to read any data from array, you access to the address and the program will go to RAM and get the value for us.
- We don't use really the address but we use the *index* (the number of the value in the array and we start from 0)
	- So if we want to Access the first element, we will use `index = 0`
- We can retrieve data at array with for or while loops 

![[Pasted image 20240503123159.png]]
## Writing Data to an Array (Fixed)
- __It will take O(1)__
- We have two types of arrays (__Fixed__ and __Dynamic__)
- We cannot add new values in fixed because we don't know if the RAM is empty or not.

![[Pasted image 20240503123858.png]]
- And we also cannot add value at any empty address, it should be after last value in our array

## Remove a value
- لما بنتكلم اننا هنمسح عنصر في ال static array مش بيبقا معناه اني اعمله deallocate لأن دا مستحيل 
- بس بيبقا معناها اني بس هعمله ==Overriding== وأغير قيمته لصفر مثلًا وببقا مش مهتم بيها بعد كدا
- __It will take O(1)__
- عشان انت كل اللي بتعمله انك بتكتب واحنا قولنا الكتابة مش بتاخد حاجة

![[Pasted image 20240624150510.png]]
## Insert value at the beginning or at middle
- هتبقا عملية مش سهلة زي إني أضيف فالأخر (Not efficient )
  لأن انت ==هتحتاج تعمل shift== لكل ال values اللي بعدها
- هتحتاج ت shift القيم اللي بعدها الأول (من الآخر للأول) 
- بعدين تحط القيمة بتاعك فالمكان المحدد
- __It will take O(n)__
- نفس المشكلة لو جينا ==نحذف== أي قيمة فالأول أو فالنص

>[!Multi-Column]
> >![[Pasted image 20240705145240.png]]
> 
> > ![[Pasted image 20240705145451.png]]

## Summary
![[Pasted image 20240705145627.png]]
## Code
```python
# Insert n into arr at the next open position.
# Length is the number of 'real' values in arr, and capacity
# is the size (aka memory allocated for the fixed size array).

def insertEnd(arr, n, length, capacity):
	if length < capacity:
		arr[length] = n

# Remove from the last position in the array if the array
# is not empty (i.e. length is non-zero).
def removeEnd(arr, n, length, capacity):
	if length > 0:
		# Overwrite last element with some default value.
        # We would also the length to decreased by 1.
		arr[length] = 0

# Insert n into index i after shifting elements to the right.
# Assuming i is a valid index and arr is not full.
def insertMiddle(arr, i, n, length):
	for index in range(length -1, i - 1, -1):
		# Shift starting from the end to i.
		arr[index + 1] = arr[index]
	# Insert at i
	arr[i] = n

# Remove value at index i before shifting elements to the left.
# Assuming i is a valid index.
def removeMiddle(arr, i, length):
	for index in range(i + 1, length):
		# Shift starting from i + 1 to end.
		arr[index - 1] = arr[index]
	# No need to 'remove' arr[i], since we already shifted

def printArr(arr, capacity):
	for i in range(capacity):
		print(arr[i])
```

# Dynamic Arrays

> [!important]
> JavaScript and Python is not having static arrays only dynamic arrays

- بتتغير وأقدر أزود حجمها وأضيف فيها عناصر زي ما أنا عايز
- بيبقا فيها زي Pointer على آخر index عندي أنا دخلته
## Push
- بضيف قيمة جديدة في آخر ال array
- __It will take O(1)__ بسبب حوار البوينتر
- ال Array مثلًا في البداية بيبقا مسموحلها انك تدخل فيها 10 عناصر حتى لو dynamic ودا ==الCapacity== بتاعها
- لو حاولت أ Push عنصر زيادة بقا في الآخر وهي كاملة إيه اللي هيحصل؟
	- بكل بساطة هيعمل Array جديدة ب Capacity ضعف ال Capacity القديمة (3 * 2 = 6)
	- هينقل كل العناصر القديمة في الجديدة اللي أكيد مكانها في ال memory اختلف
	- بتعمل deallocate لل Array القديمة عشان تفضي مساحتها
	- وهكذا
- العملية دي بقا بتاخد **O(n)** لأن إنك تعمل Array جديدة بتاخد الوقت دا وكمان إني أحط القيم القديمة بتاخد **O(n)** انما عملية ال Push نفسها مش بتاخد إلا **O(1)**
- بسبب حوار الوقت دا كل مرة بنضاعف ال Capacity مش بس بنزود واحد للقيمة الجديدة لأن كل مرة هياخد وقت **O(n)** 
  وبرضو مزودنهاش عالفاضي وخلاص عشان ميبقاش فيه مساحة فاضية كتير ودا مش كويس لل OS

![[Pasted image 20240706153103.png]]

- We talked about it at [[Amortized analysis]], So we can say __It will take O(1)__
## Pop
- أقدر أشيل آخر عنصر في ال Array
- __It will take O(1)__
## Summary
Same as Static arrays
![[Pasted image 20240705145627.png]]
## Code
### Python
```python
# Python arrays are dynamic by default, but this is an example of resizing.
class Array:
	def __init__(self):
		self.capacity = 2
		self.length = 0
        self.arr = [0] * 2 # Array of capacity = 2

	# Insert n in the last position of the array
	def pushback(self, n):
		if self.length == self.capacity:
			self.resize()
		#insert at next empty position
		self.arr[self.length] = n
		self.length += 1

	def resize(self):
	    # Create new array of double capacity
		self.capacity *= 2
		newArr = [0] * self.capacity
		# Copy elements to newArr
        for i in range(self.length):
            newArr[i] = self.arr[i]
        self.arr = newArr
        
    # Remove the last element in the array
    def popback(self):
        if self.length > 0:
            self.length -= 1
    
    # Get value at i-th index
    def get(self, i):
        if i < self.length:
            return self.arr[i]
        # Here we would throw an out of bounds exception

    # Insert n at i-th index
    def insert(self, i, n):
        if i < self.length:
            self.arr[i] = n
            return
        # Here we would throw an out of bounds exception       

    def print(self):
        for i in range(self.length):
            print(self.arr[i])
        print()
```
