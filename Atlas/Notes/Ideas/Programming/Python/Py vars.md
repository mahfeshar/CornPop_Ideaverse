---
up:
  - "[[Py Built in Functions]]"
related:
  - "[[Py __dict__]]"
created: 2024-04-26
tags:
---
- The `vars()` function returns the [[Py __dict__]] attribute of an object.
- Syntax: `vars(_object_)`
	- object: Any object with a `__dict__`attribute

```python
class Person:  
  name = "John"  
  age = 36  
  country = "norway"  
  
x = vars(Person)
# {'__module__': '__main__', 'name': 'John', 'age': 36, 'country': 'norway', '__dict__': <attribute '__dict__' of 'Person' objects>, '__weakref__': <attribute '__weakref__' of 'Person' objects>, '__doc__': None}

y = Person()
print(vars(y)) # {}
```