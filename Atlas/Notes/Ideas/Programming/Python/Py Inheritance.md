---
up:
  - "[[Py OOP]]"
related:
  - "[[Py Encapsulation]]"
  - "[[Py Abstraction]]"
  - "[[Py Polymorphism]]"
created: 2024-04-26
tags:
---
# Inheritance
- We talked before about [[Inheritance]]
#### Syntax
```python
# Base class
class BaseClassName:

# Derived **class**
class DerivedClassName(BaseClassName): # At SAME module
class DerivedClassName(modname.BaseClassName) # At ANOTHER module

#using it
x = DerivedClassName(attributes)
```

> [!Note] Private
> The child class inherits everything but if the private things cannot.
- We should first write `__init__` at child class and don't  forget any of instance variables for parent
```python
class A:
	def __init_(self, n='corn'):
		self.name = n
class B(A):
	def __init__(self, n):
		self.name = n
	# def __init__(self,roll): # ERROR
```
#### `super() function`
- It's a built-in function that returns the objects represent the parent class
```python
class B(A):
	def __init(self, n, age):
		super().__init__(n)
		self.age = age
	# Add methods
	def hello(self):
		print('Hello')
```
- we can add more [[Py Instance methods]] and [[Py Instance Attributes]] for child
>[!note]
>If we used [[Py isinstance]] function with child and check if it (Parent Class), it will me that's TRUE
#### Multiple Inheritance
- We can define child class with multiple base classes
```python
class DerivedClass(Base1, Base2, Base3):
```
- If an attribute not in `DerivedClass`, it is searched for in `Base1` then in the base classes of `Base1` then `Base2` and so on.
---
#### Base Class
- The model that all classes at our program inherit from
- We put at it the methods and attributes that we want all classes have
- We can override methods at the child class
```python
class BaseModel():
	def __init__(self):
		self.fave_color = "green"

class MyClass(BaseModel):
	pass
```
#### Important
- We can use [[Py dir]] built-in function to list all attributes and method of classes and instances 
- All classes inherit from the built-in class named `object`
- `object` is the default base class, Why?
	- **Provides common functionality** like `__str__` or `__eq__` We call it [[Py Magic methods]]
	- **Consistent behaviour:** Inheriting from `object` ensures a baseline level of functionality for all classes, making them behave more uniformly
	- **Simplifies object-oriented programming:** With `object` as the root, Python maintains a clear object hierarchy
```python
class Person:
  def __init__(self, name):
    self.name = name

# Inherits from object implicitly
person1 = Person("Alice")

print(person1)  # Uses __str__() method inherited from object
```