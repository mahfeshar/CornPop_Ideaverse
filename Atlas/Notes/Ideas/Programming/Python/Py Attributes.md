---
up:
  - "[[Py class]]"
related:
  - "[[Py methods]]"
created: 2024-04-26
tags:
  - note/develop🍃
---
- Attributes are created inside a class definition.
- We have two types of attributes:
	- The attributes which is defined in constructor called [[Py Instance Attributes]]
	- The attributes that is defined outside the constructor called [[Py Class Attributes]]
## Arbitrary attributes
- We can dynamically create arbitrary اعتباطي new attributes for existing instances of a class. 
```python
class Robot:
	pass
x = Robot()
y = Robot()
x.name = "Corn"
x.build_year = "1979"
y.name = "Caliban"
y.build_year = "1993"
print(x.name) # Marvin
print(y.build_year) # 1993
```
- We can use [[Py setattr]] function to set an attribute on an object at runtime.
```python
setattr(Robot, "name", 'Corn')
print(Robot.name) # Corn
```
>[!note]
They are the same but, `setattr` offers more explicit control so it used with attributes with complex logic and Direct assignment is simpler but can make code less readable

> [!danger]
> The arbitrary attributes will make code harder so **don't  OVERUSE it**


## How to print attributes
- We can use [[Py __dict__]] to show all class attributes or just object attributes.
- We can use it with [[Py class]] and it will print all things in class 
```python
# Using with class
class Temp:
	x = 1

print(Temp.__dict__)
# {'__module__': '__main__', 'x': 1, '__dict__': <attribute '__dict__' of 'Temp' objects>, '__weakref__': <attribute '__weakref__' of 'Temp' objects>, '__doc__': None}
```
- We also can use it with [[Py object]] but it will print all attributes for this object not for class
```python
class Temp:
    x = 1
    def __init__(self):
        self.name = 'corn'

y = Temp()
y.age = 15
print(y.__dict__) # {'name': 'corn', 'age': 15}
```

- You can see the second replay here [python - Explain __dict__ attribute - Stack Overflow](https://stackoverflow.com/questions/19907442/explain-dict-attribute)
![[Py __dict__#^fe593a]]

- For that we should use [[Py vars]]
### Example
```python
class Person:
    age = 30  # Class variable

    def __init__(self, name):
        self.name = name  # Instance attribute

person = Person("Alice")
person.job = "Software Developer"  # Dynamically adding an attribute

# Accessing attributes
print(f"Class variable: {Person.age}") # Class variable: 30

print(f"Instance attribute (using dot notation): {person.name}") 
# Instance attribute (using dot notation): Alice

print(f"Instance attribute (using __dict__{person.__dict__['name']}")
# Instance attribute (using __dict__): Alice

# Accessing all attributes using vars()
all_attributes = vars(person)
print(f"All attributes (using vars()): {all_attributes}")
# All attributes (using vars()): {'name': 'Alice', 'job': 'Software Developer'}
```
## Access attributes without errors
>[!error]
> If you try to access a non-existing attribute, you will raise an AttributeError.

- You can use [[Py getattr]] to prevent this exception (if you provide a default value as the third argument)
```python
getattr(x, 'energy', 100) #100
```