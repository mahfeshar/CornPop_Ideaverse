---
up:
  - "[[Py methods]]"
related:
  - "[[Py Class methods]]"
  - "[[Py Instance methods]]"
  - "[[Py Magic methods]]"
created: 2024-05-15
---
- It takes __no parameters__, I mean `cls` or `self` but it can take parameters
- مبقدرش تعدل على أي حاجة في الclass او ال Object
- Its bound to the class not instance
- Used when doing something doesn't have access to object or class but related to class
- We use it to make utility functions; It helps us to complete mission
- It also called helper methods
```python
class Math:
    @staticmethod
    def add(x, y):
        return x + y
    
    @staticmethod
    def add5(num):
        return num + 5
    
    @staticmethod
    def add10(num):
        return num + 10
    @staticmethod
    def PI():
        return 3.14
    
x = Math.add(10, 5)
y = Math.add5(x)
z = Math.add10(y)
print(x, y, z)
```