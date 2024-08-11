---
up:
  - "[[Py Attributes]]"
related:
  - "[[Py Instance Attributes]]"
created: 2024-04-26
tags:
  - note/develop🍃
---
- Class Attributes: Attributes defined *outside the constructor*
- بتبقا متشاركة مع كل ال Objects بتاع الكلاس (same attribute for all objects)

- لازم أحدد قيمة من الأول
- لما بنيجي نستخدمه جوا ال methods بنكتب اسم ال class مش ال self ولو برا مش بنكتب حاجة
- We can access class attribute from any object or from class

```python
class Member:

  #Class Attributes
  not_allowed_names = ["Hell", "Shit", "Baloot"]
  users_num = 0

  def __init__(self, first_name, middle_name, last_name, gender):
	#Instance attributes
    self.fname = first_name
    self.mname = middle_name
    self.lname = last_name
    self.gender = gender
    Member.users_num += 1  
    # If we want to use class attribute, we should write class name before it

member_one = Member("Osama", "Mohamed", "Elsayed", "Male")
member_two = Member("Ahmed", "Ali", "Mahmoud", "Male")
member_three = Member("Mona", "Ali", "Mahmoud", "Female")
member_four = Member("Shit", "Hell", "Metal", "DD")

print(member_one.users_num) # 4
print(member_two.users_num) # 4
# We can access class attribute from any object
print(Member.users_num) # 4
# And We can access it from Class too
