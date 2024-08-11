---
up:
  - "[[Py Built in Functions]]"
related:
  - "[[Py Attributes]]"
  - "[[Py getattr]]"
created: 2024-04-26
tags:
  - note/develop🍃
---
- The `setattr()` function sets the value of the specified attribute of the specified object.
- Syntax: `setattr(object, attribute, value)`
	- object: An object (Required)
	- attribute: The name of the attribute you want to set (Required)
	- value: The value you want to give the specified attribute (Required)
## Example
```python
class Person:  
  name = "John"  
  age = 36  
  country = "Norway"  
  
setattr(Person, 'age', 40)
```
## Related Pages

- The [delattr()](https://www.w3schools.com/python/ref_func_delattr.asp) function, to remove an attribute
- The [getattr()](https://www.w3schools.com/python/ref_func_getattr.asp) function, to get the value of an attribute
- The [hasattr()](https://www.w3schools.com/python/ref_func_hasattr.asp) function, to check if an attribute exist