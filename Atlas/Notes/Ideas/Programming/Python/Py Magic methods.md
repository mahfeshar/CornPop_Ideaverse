---
up:
  - "[[Py methods]]"
related: 
created: 2024-04-26
tags:
  - note/develop🍃
Link: https://www.geeksforgeeks.org/dunder-magic-methods-python/
---
- It have another name called **Dunder**
- It's methods starting and ending with double underscores ‘\_\_’.
- We can override them with [[Py Polymorphism]] concept
- You can see all of them by using [[Py dir]]
```python
print(dir(int))

# ['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '_...
```
## Some Magic Methods:

### **Initialization and Construction**
- [[Py __init__]]
### **Comparison magic methods**
```python
def __eq__(self, other):
	"""Define the == comparision to a Square."""
	return self.area() == other.area()

def __ne__(self, other):
	"""Define the != comparison to a Square."""
	return self.area() != other.area()

def __lt__(self, other):
	"""Define the < comparison to a Square."""
	return self.area() < other.area()

def __le__(self, other):
	"""Define the <= comparison to a Square."""
	return self.area() <= other.area()

def __gt__(self, other):
	"""Define the > comparison to a Square."""
	return self.area() > other.area()

def __ge__(self, other):
	"""Define the >= compmarison to a Square."""
	return self.area() >= other.area()
```

### **Other**
- [[Py __str__]]
- [[Py __repr__]]
- [[Py __class__]]
- [[Py __len__]]
