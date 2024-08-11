---
up:
  - "[[Py Built in Functions]]"
related:
  - "[[Py __repr__]]"
created: 2024-04-26
tags:
  - note/develop🍃
---
- The `eval()` function evaluates the specified expression, if the expression is a legal Python statement, it will be executed.
- Syntax: `eval(_expression_, _globals_, _locals_)`
	- expression: A String, that will be evaluated as Python code
	- globals: A dictionary containing global parameters (*Optional*)
	- locals: A dictionary containing local parameters (*Optional*)
```python
x = 'print(55)'  
eval(x)

```