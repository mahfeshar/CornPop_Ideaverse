---
up:
  - "[[Py Built in Functions]]"
related:
  - "[[Py all]]"
created: 2024-04-27
---
- The `any()` function returns True if any item in an iterable are true, otherwise it returns False.
- If the iterable object is empty, the `any()` function will return False.
- Syntax: `any(iterable)`
	- iterable: An iterable object ([[Py list]], [[Py tuple]], [[Py dictionary]])
### Examples:
```python
mytuple = (0, 1, False)  
x = any(mytuple) # True 

myset = {0, 1, 0}  
x = any(myset)

mydict = {0 : "Apple", 1 : "Orange"}  
x = any(mydict)
```