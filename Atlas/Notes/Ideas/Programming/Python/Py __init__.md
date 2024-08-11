---
up:
  - "[[Py class]]"
related:
  - "[[Py Magic methods]]"
created: 2024-04-26
tags: []
---
- It makes a **constructor** for the class
- `__init__` is a method which is automatically called after an instance has been created
```python
class Robot:
	def __inti__(self, name=None):
		self.name = name
	def say_hi(self):
		if say_hi:
			print("Hi, I am " + self.name)
		else:
			print("Hi, I am a robot without a name")
x = Robot()
x.say_hi() # Hi, I am a robot without a name
y = Robot("Marvin")
y.say_hi() # Hi, I am Marvin
```
- `self` refer to the current instance created from the class and must be first parameter