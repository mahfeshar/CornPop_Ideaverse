[Sessions - new | Intranet](https://intranet.alxswe.com/projects/260)
Problem 11
Topic: [[Py File Handling]]

---

Write a class `Student` that defines a student by: (based on `10-student.py`)

- Public instance attributes:
    - `first_name`
    - `last_name`
    - `age`
- Instantiation with `first_name`, `last_name` and `age`: `def __init__(self, first_name, last_name, age):`
- Public method `def to_json(self, attrs=None):` that retrieves a dictionary representation of a `Student` instance (same as `8-class_to_json.py`):
    - If `attrs` is a list of strings, only attributes name contain in this list must be retrieved.
    - Otherwise, all attributes must be retrieved
- Public method `def reload_from_json(self, json):` that replaces all attributes of the `Student` instance:
    - You can assume `json` will always be a dictionary
    - A dictionary key will be the public attribute name
    - A dictionary value will be the value of the public attribute
- You are not allowed to import any module

Now, you have a simple implementation of a serialization and deserialization mechanism (concept of representation of an object to another format, without losing any information and allow us to rebuild an object based on this representation) [[Py json]]

## Shell
```python
guillaume@ubuntu:~/0x0B$ cat 11-main.py 
#!/usr/bin/python3
import os
import sys

Student = __import__('11-student').Student
read_file = __import__('0-read_file').read_file
save_to_json_file = __import__('5-save_to_json_file').save_to_json_file
load_from_json_file = __import__('6-load_from_json_file').load_from_json_file

path = sys.argv[1]

if os.path.exists(path):
    os.remove(path)

student_1 = Student("John", "Doe", 23)
j_student_1 = student_1.to_json()
print("Initial student:")
print(student_1)
print(type(student_1))
print(type(j_student_1))
print("{} {} {}".format(student_1.first_name, student_1.last_name, student_1.age))


save_to_json_file(j_student_1, path)
read_file(path)
print("\nSaved to disk")


print("Fake student:")
new_student_1 = Student("Fake", "Fake", 89)
print(new_student_1)
print(type(new_student_1))
print("{} {} {}".format(new_student_1.first_name, new_student_1.last_name, new_student_1.age))


print("Load dictionary from file:")
new_j_student_1 = load_from_json_file(path)

new_student_1.reload_from_json(j_student_1)
print(new_student_1)
print(type(new_student_1))
print("{} {} {}".format(new_student_1.first_name, new_student_1.last_name, new_student_1.age))

guillaume@ubuntu:~/0x0B$ ./11-main.py student.json
Initial student:
<11-student.Student object at 0x7f832826eda0>
<class '11-student.Student'>
<class 'dict'>
John Doe 23
{"last_name": "Doe", "first_name": "John", "age": 23}
Saved to disk
Fake student:
<11-student.Student object at 0x7f832826edd8>
<class '11-student.Student'>
Fake Fake 89
Load dictionary from file:
<11-student.Student object at 0x7f832826edd8>
<class '11-student.Student'>
John Doe 23
guillaume@ubuntu:~/0x0B$ cat student.json ; echo ""
{"last_name": "Doe", "first_name": "John", "age": 23}
guillaume@ubuntu:~/0x0B$ 
```
## Solve
```python
class Student:
	def __init__(self, first_name, last_name, age):
		self.first_name = first_name
		self.last_name = last_name
		self.age = age

    def to_json(self, attrs=None):
		if (isinstance(attrs, list) and
				all(isinstance(ele, str) for ele in attrs)):
			return {k: getattr(self, k) for k in attrs if hasattr(self, k)}
		return self.__dict__

	def reload_from_json(self, json):
        for k, v in json.items():
            setattr(self, k, v)
```
- We made [[Py class]] with [[Py Instance Attributes]] in [[Py __init__]] and we made [[Py Instance methods]]
- We used [[Py isinstance]] to check if attrs is list or not, and then we use [[Py all]] that return true if all  of iterable inside it true, and we used [[Py getattr]] to get attributes from instance
- We used [[Py setattr]] to change value for [[JSON]]