---
up:
  - "[[Py Built in Functions]]"
related:
  - "[[Py __dict__]]"
  - "[[Py vars]]"
created: 2024-04-29
tags:
---
- We use it to know what's in class? (All [[Py methods]] and [[Py Attributes]])
- It returns a list containing all the names defined within a class or object.
```python
class MyClass:
	name = 'Corn'
	def greet(self):
		print('Hello')
obj = MyClass()

# List attributes and methods of the class 
class_members = dir(MyClass) 
# ['__class__', '__delattr__', ..., 'greet', 'name']
# List attributes of the object instance 
instance_members = dir(obj)
['__class__', '__delattr__', ..., 'greet']
```
When I see it I remember [[Py __dict__]] and [[Py vars]] because it is similar to them.
[[Py dir, __dict__ vs vars]]