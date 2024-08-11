---
up:
  - "[[Py Built in Functions]]"
related:
  - "[[Py setattr]]"
  - "[[Py Attributes]]"
created: 2024-04-26
tags: []
---
- The `getattr()` function returns the value of the specified attribute from the specified object.
- Syntax: `getattr(_object_, _attribute_, _default_)`
	- object: An object (Required)
	- attribute: The name of the attribute you want to get the value from
	- default: The value to return if the attribute does not exist (Optional)

>[!error]
> If you didn't add default, and the attribute isn't exist, it will give you AttributeError

```python
class Person:
  name = "John"
  age = 36
  country = "Norway"

x = getattr(Person, 'size')
print(x) # error
x = getattr(Person, 'size', 50)
print(x) # 50
```