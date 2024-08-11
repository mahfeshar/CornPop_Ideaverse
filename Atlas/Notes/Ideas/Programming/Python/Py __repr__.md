---
up:
  - "[[Py Magic methods]]"
related:
  - "[[Py __str__]]"
  - "[[Py __len__]]"
  - "[[Py __init__]]"
  - "[[Py __dict__]]"
  - "[[Py __class__]]"
created: 2024-04-26
tags:
---
- It's for unambiguous representation for development and debugging. 
  (could be used to recreate the object)
- It's generate output for **developer**
```shell
>>> help(repr)
'Return the canonical العنوان الأساسي string representation of the object.'
```

```python
>>> repr(123)
'123'
>>> repr('Corn')
"'Corn'"
```
- It should be possible to recreate our object using [[Py eval]]
```python
x = 'corn'
print(repr(x)) # 'Corn': STRING
print(eval(repr(x))) # Corn: Some characters can't use it again
```
>[!Note]
>If I defined it and I didn't defined [[Py __str__]], the str will have same output.

I defined the differences between them here, [[Py str vs repr]]