---
up:
  - "[[Py Magic methods]]"
related:
  - "[[Py __repr__]]"
  - "[[Py __str__]]"
created: 2024-04-26
tags:
  - note/develop🍃
---
# str vs repr
[[Py __str__]], [[Py __repr__]]

- `__str__` for readable output to users, `__repr__` for unambigous representation for development and debugging.
- unambigous representation that could be used to recreate the object.
```python
>>> help(str)
'Create a new string object from the given object.'
>>> help(repr)
'Return the canonical string representation of the object.'
```
they seem to be fairly similar. Let’s see them in action:
```python
>>> str(123)
'123'
>>> repr(123)
'123'
```
Alright no difference for now.
```python
>>> str('Python')
'Python'
>>> repr('Python')
"'Python'"
```

A second pair of quotes around our string. Why?  
With the return value of _repr()_ it should be possible to recreate our object using [[Py eval]](). This function takes a string and evaluates it’s content as Python code.

```python
h = 'python'  
print(str(h)) # python
print(repr(h)) # 'python'
# print(eval(str(h))) #error  
print(eval(repr(h))) # python
```
### str
- Gives a human-readable output of the object
- generate output for end user
```python
class Robot:  
    def __str__(self):  
        return f"This is my class"

x = Robot()
print(x) # This is my class
# or print(str(x))
# Without str: <__main__.Robot object at 0x000002587F477520>

print(repr(x)) # <__main__.Robot object at 0x000002587F477520>
```
### repr
It also produces a string representation.
- need code that reproduces object
- generate output for developer

If a class has a `__str__` method, the method will be used for an instance x of that class, if either the function str is applied to it or if it is used in a print function. 
`__str__` will not be used, if repr is called, or if we try to output the value directly in an interactive Python shell.

Otherwise, if a class has only the `__repr__` method and no `__str__` method, `__repr__` will be applied in the situations, where `__str__` would be applied, if it were available:
```python
class A:
    def __repr__(self):
        return "42"
a = A()
print(repr(a)) # 42
print(str(a)) # 42
```
- لو عرفت ال str وناديت على repr أو جربت تعمل output للclass من الshell مش هياخد الحاجة اللي انت معرفها
- لو عرفت ال repr القيمة بتاع ال str لما تشوفها هتبقا نفس اللي عرفتها
- لو عرفت الاتنين سوا فكل واحدة لما هتنديلها هتشوف القيمة اللي انت معرفها فيها