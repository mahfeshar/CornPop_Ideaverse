---
up:
  - "[[OOP]]"
related: 
created: 2024-10-10
---

![[Pasted image 20240218092537.png]]

*[[Encapsulation]]* is seen as the bundling تجميع of data with the methods that operate on that data. (setter and getter)
*Information hiding* is the principle that some internal information or data is "hidden", so that it can't be accidentally changed.

Data encapsulation via methods doesn't necessarily mean that the data is hidden. You might be capable of accessing and seeing the data anyway, but using the methods is recommended.

*Data [[abstraction]]* is present, if both data hiding and data encapsulation is used. In other words, data abstraction is the broader term:
_Data Abstraction = Data Encapsulation + Data Hiding_

Encapsulation is often accomplished by providing two kinds of methods for attributes: 
The methods for retrieving or accessing the values of attributes are called getter methods. Getter methods do not change the values of attributes, they just return the values. 
The methods used for changing the values of attributes are called setter methods.

```python
class Robot:
	def __init__(self, name=None):
		self.name = name
	def say_hi(self):
		if self.name:
            print("Hi, I am " + self.name)
        else:
            print("Hi, I am a robot without a name")
	def set_name(self, name):
		self.name = name
	def get_name(self):
		return self.name
```