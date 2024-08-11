---
up:
  - "[[Py Built in Functions]]"
related: 
created: 2024-04-27
tags: []
---
- It used to check if an [[Py object]] belongs to a particular [[Py class]] or type. 
- It returns `True` if the object is an instance of the specified class or any of its subclasses, and `False` otherwise.
- Syntax: `isinstance(object, classinfo)`
```python
#isinstance(_object_, _type_)

x = 5 
print(isinstance(x, int)) # True, because x is an instance of int class 
print(isinstance(x, str)) # False, because x is not an instance of str class

x = isinstance(5, int) #True

#Check if "Hello" is one of the types described in the type parameter:
x = isinstance("Hello", (float, int, str, list, dict, tuple))
```