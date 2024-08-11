---
up:
  - "[[Py OOP]]"
related:
  - "[[Py Encapsulation]]"
  - "[[Py Inheritance]]"
  - "[[Py Abstraction]]"
created: 2024-04-26
tags: []
---
- We explained before about [[Polymorphism]]
- An example: That we can use `len()` function with different objects 
- It means that we can use same name of function for different classes and do same logic
- It's related to [[Py Inheritance]] because we can't make overloading or overriding without it.
```python
class Vehicale:
	def __init__(self, brand):
		self.brand = brand
	def move(self):
		print("Move!")
class Boat(Vehicale):
	def move(self):
		# Call the base class method (optional)
		super().move()
		print("Sail!")
```