---
up:
  - "[[Py Magic methods]]"
related:
  - "[[Py __len__]]"
  - "[[Py __str__]]"
  - "[[Py __dict__]]"
  - "[[Py __init__]]"
  - "[[Py __repr__]]"
created: 2024-04-26
tags:
---

- Tells us which class that object belongs to
```python
aList = [1, 2]  
print(aList.__class__) # <class 'list'>
print(dir(aList)) # dir to know all methods and attributes
```