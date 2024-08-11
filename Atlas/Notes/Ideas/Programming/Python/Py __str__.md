---
up:
  - "[[Py Magic methods]]"
related:
  - "[[Py __len__]]"
  - "[[Py __dict__]]"
  - "[[Py __repr__]]"
  - "[[Py __init__]]"
  - "[[Py __class__]]"
created: 2024-04-26
tags:
---

- It's for readable output to users (a human-readable output of the object)
```shell
>>> help(str)
'Create a new string object from the given object.'
```

>[!error]
>We can't use it again with eval because it's just output for user


```python
print(str('Corn')) # Corn : Some characters not string
print(eval(str('Corn'))) # NameError
```

>[!Note]
If I defined it and I didn't define [[Py __repr__]], repr will NOT take the output for str and will be default value

I defined the differences between them here, [[Py str vs repr]]