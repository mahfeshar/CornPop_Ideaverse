---
up:
  - "[[Py Attributes]]"
related:
  - "[[Py Class Attributes]]"
created: 2024-04-26
tags:
---
## Instance Attributes
- Instance Attributes: Defined inside the constructor [[Py __init__]]
- هتبقا موجودة في كل ال Objects اللي هتتعمل من ال class دا بس القيم هتختلف بالقيم اللي هديهالها
```python
class Member:
  def __init__(self, first_name, middle_name, last_name):
    self.fname = first_name #instance attrinutes
    self.mname = middle_name
    self.lname = last_name

member_one = Member("Osama", "Mohamed", "Elsayed")
member_two = Member("Ahmed", "Ali", "Mahmoud")
member_three = Member("Mona", "Ali", "Mahmoud")

# print(dir(member_one))

print(member_one.fname, member_one.mname, member_one.lname)
print(member_two.fname)
print(member_three.fname)
```