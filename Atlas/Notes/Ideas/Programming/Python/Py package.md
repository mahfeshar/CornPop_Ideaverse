---
up:
  - "[[Py library]]"
related:
  - "[[Py Module]]"
created: 2024-04-28
tags:
  - note/develop🍃
---
## What is a Python Package?
![[Pasted image 20240428153217.png]]
- A multiple modules will make [[Py library]]
- It's a same as a directory containing other sub-packages or [[Py Module]] in a structured way and making the access for them easy.
- File organization is really important in a big project. This means for Python: packages everywhere.
## Creating a Python Package
- The directory that contains the `__init__.py` file is defined as a Package. (**Must**)
	- This file can be *empty*
- It can be imported the same way as a module.
- The `__init__` will be call, If you import the package
### `__all__`
- A common thing to define in the `__init__.py` is the `__all__` variable.
- This overwrites what modules and functions should be imported when a user runs an import statement in the form `from mypackage import *`.
- By default, Python does **not** import modules from a package. So if we changed the first line in our `calculator.py` file to import everything from `operations`, it would not work.
```python
from operation import * 
# will cause error
```
- But if we add the following line to `operations/__init__.py`:
```python
__all__ = ['divider', 'multiplier']
```
### Example
![[Pasted image 20240428154750.png]]
## Access Package
![[Pasted image 20240428155444.png]]

To read: [What is \`\_\_init\_\_.py\` for in Python? | Sentry](https://sentry.io/answers/what-is-init-py-for-in-python/#:~:text=In%20Python%20projects%2C%20if%20you,imported%20into%20other%20Python%20files)
