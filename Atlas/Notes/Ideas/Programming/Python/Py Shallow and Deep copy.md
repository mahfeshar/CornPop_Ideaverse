---
up:
  - "[[Python MOC]]"
related: 
created: 2024-07-11
---

## Using =
أول حاجة تعرفها انك لو استخدمت علامة ال = مع الlists مثلًا دا مش بيعمل نسخة منه دا بيغير اسمها بس والاسم الجديد هيبقا بيشاور على الList القديمة
```python
list = [1, 2, 3, 4, 5]
new_list = list
list[0] = 9
new_list[1] = 10
print('List: ', list) #List:  [9, 10, 3, 4, 5]
print('List ID: ', id(list)) #List ID:  2540528390720
print('New List: ', new_list) # New List:  [9, 10, 3, 4, 5]
print('New List ID: ', id(new_list)) # New List ID:  2540528390720: SAME
```
وبالطريقة دي انت مش بتعمل نسخة ولا حاجة انت مجرد بتشاور عليه بس زي ال [[Pointer]]
# Copy
We have 2 types of copy: Shallow, Deep
```python
import copy

copy.copy #shallow copy
copy.deepcopy #deep copy
```
## Shallow Copy
- بتعمل نسخة من الObject بس مش بتعمل نسخة من الobjects اللي جوا ال object دا (في حالة object جوا object)
- A shallow copy creates a new object but does not recursively copy the objects within it. Instead, it **creates references** to the objects found in the original. 
- This means that changes made to the original object's nested objects will also be reflected in the shallow copy and vice versa.
```python
import copy

# Original list
original_list = [[1, 2, 3], [4, 5, 6]]
# Shallow copy
shallow_copied_list = copy.copy(original_list)

# Modify the nested list in the original
original_list[0][0] = 0

# Both the original and the shallow copy are affected
print(original_list)         # Output: [[0, 2, 3], [4, 5, 6]]
print(shallow_copied_list)   # Output: [[0, 2, 3], [4, 5, 6]]
```
- It simply **copies references** to the objects contained in the original list. 
- This means that if the elements of the list are mutable objects [[Mutable vs Immutable]] (like lists themselves), changes made to these mutable objects within the original list **will also be reflected in the copied list**, *because they are referring to the same objects in memory*.

- However, **if you change the reference itself** (e.g., assign a new object to an element in the copied list), it won't affect the original list, as the references are separate.
```python
import copy

# Original list with mutable objects (sublists)
original_list = [[1, 2, 3], [4, 5, 6]]

# Shallow copy
shallow_copied_list = copy.copy(original_list)

# Modify an element in the copied list
shallow_copied_list[1] = [7, 8, 9]

# Only the copied list is affected, not the original
print(original_list)           # Output: [[0, 2, 3], [4, 5, 6]]
print(shallow_copied_list)     # Output: [[0, 2, 3], [7, 8, 9]]
```
## Deep Copy
- بتعمل نسخة من الobject ومن اللي جوا الobject كمان
- A deep copy creates a new object and recursively **copies all the objects** found within the original object. 
- This means that changes made to the original object's nested objects will not affect the deep copy, and vice versa.
```python
import copy

# Original list
original_list = [[1, 2, 3], [4, 5, 6]]
# Deep copy
deep_copied_list = copy.deepcopy(original_list)

# Modify the nested list in the original
original_list[0][0] = 0

# Only the original is affected, not the deep copy
print(original_list)        # Output: [[0, 2, 3], [4, 5, 6]]
print(deep_copied_list)     # Output: [[1, 2, 3], [4, 5, 6]]
```