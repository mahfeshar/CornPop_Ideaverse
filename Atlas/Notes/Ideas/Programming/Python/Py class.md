---
up:
  - "[[Py OOP]]"
related:
  - "[[Py object]]"
created: 2024-04-26
tags:
  - note/develop🍃
---
- Class is the blueprint or constructor of the [[Py object]]
- Everything is a class in python: functions and methods are values just like lists, integers or floats.
- Class name written with PascalCase (UpperCamelCase) Style
- Class may contains [[Py Attributes]] and [[Py methods]]
```python
class MyClass:
	x = 5 # Attribute
```
- We have function called [[Py __init__]] which is **Constructor** for the class
	- When creating object python look for it.
- **Instance**: Object created from class and have their methods and attributes