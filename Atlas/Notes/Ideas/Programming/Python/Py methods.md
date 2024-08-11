---
up:
  - "[[Py class]]"
related:
  - "[[Py Attributes]]"
created: 2024-04-26
tags:
  - note/develop🍃
---
- Method in Python is *just* a [[Py function]] which is defined inside a class.
```python
class Person:  
  def __init__(self, name, age):  
    self.name = name  
    self.age = age  
  
  def myfunc(self):  
    print("Hello my name is " + self.name)  
  
p1 = Person("John", 36)  
p1.myfunc() # calling method
```
- We have different types for methods:
	- [[Py Instance methods]]
	- [[Py Class methods]]
	- [[Py Static methods]]
- We have a custom type of methods called [[Py Magic methods]] or **Dunder**