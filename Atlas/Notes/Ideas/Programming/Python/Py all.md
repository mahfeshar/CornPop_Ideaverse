---
up:
  - "[[Py Built in Functions]]"
related:
  - "[[Py any]]"
created: 2024-04-27
---
- It returns True if all items in an iterable are true, otherwise it returns False.
- If the iterable object is empty, the `all()` function also returns True.
- Syntax: `all(iterable)`
	- iterable: An iterable object (list, tuple, dictionary)

### Examples:
```python
mylist = [0, 1, 1]  
x = all(mylist) # False: 0 is false

mytuple = (0, True, False)  
x = all(mytuple) # False


```
- If we used it with [[Py dictionary]], keys not values
```python
# Check if all items in a _dictionary_ are True:
mydict = {0 : "Apple", 1 : "Orange"}  
x = all(mydict)
```