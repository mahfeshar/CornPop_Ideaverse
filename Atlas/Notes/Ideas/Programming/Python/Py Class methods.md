---
up:
  - "[[Py methods]]"
related:
  - "[[Py Magic methods]]"
  - "[[Py Instance methods]]"
  - "[[Py Static methods]]"
created: 2024-05-15
tags:
---
- Marked with `@classmethod` decorator to flag it as class method
- It takes `cls` parameter not self to **point to the class not the instance**
- It **doesn't** require creation of a class in
stance
- Used when you want to do something with the class itself
- You can edit [[Py Class Attributes]] and you can't edit [[Py Instance Attributes]]
- We can't make more than one [[Py __init__]] So we can use `classmethod` to `init` it with another arguments
- بتخليني أضحك على python واعمل أكتر من [[Py __init__|Constructor]]

```python
from datetime import date

class Student:
    def __init__(self, name, age = 0):
        self.__name = name
        self.__age = age

    def describe(self):
        print(f'My name is {self.__name} and my age is {self.__age}')

    @classmethod
    def initFromBirthYear(cls, name, birthYear):
        return cls(name, date.today().year - birthYear)

Student1 = Student('Corn', 20)
Student2 = Student.initFromBirthYear('Pop', 2003)
  
Student1.describe()
Student2.describe()
# My name is Corn and my age is 20
# My name is Pop and my age is 21
```

- أقدر أعمل functions منها كل اللي بتعمله اني أناديلها وانا بعمل object عشان يملى البيانات بحاجات مسبقة

```python
class Pizza:
    def __init__(self, ingredients):
        self.ingredients = ingredients

    def __str__(self) -> str:
        return f'{self.ingredients}'

    @classmethod
    def veg(cls):
        return cls(['mushrooms', 'olives', 'onions'])
    
    @classmethod
    def margherita(cls):
        return cls(['mozarella', 'sause'])
    
pizza1 = Pizza(['tomatoes', 'olives'])
pizza2 = Pizza.veg()
pizza3 = Pizza.margherita()

print(pizza1, pizza2, pizza3)
# ['tomatoes', 'olives'] ['mushrooms', 'olives', 'onions'] ['mozarella', 'sause']
```