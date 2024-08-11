---
up:
  - "[[Py methods]]"
related:
  - "[[Py Class methods]]"
  - "[[Py Static methods]]"
  - "[[Py Magic methods]]"
created: 2024-04-27
tags: []
---
- Instance Methods: Defined inside the constructor [[Py __init__]]
- Take self parameter which point to instance created from class. (object)
- It can freely access attributes and methods on the same object
- It can access the class itself
```python
class Member:
	def __init__(self, first_name, last_name):
		self.fname = first_name
	    self.lname = last_name

	def full_name(self):
		return f"{self.fname} {self.lname}"

member_one = Member("Mahmoud", "Feshar")
member_two = Member("Corn", "Pop")

print(member_one.full_name())
```