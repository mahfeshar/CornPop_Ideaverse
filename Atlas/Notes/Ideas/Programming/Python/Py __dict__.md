---
up:
  - "[[Py Special Attributes]]"
related:
  - "[[Py vars]]"
created: 2024-04-26
tags: []
---


> A dictionary or other mapping object used to store an object's (writable) attributes.

- It contains all the attributes which describe the object in question. It can be used to alter or read the attributes.

```python
def func():
    pass

func.temp = 1
print(func.__dict__) # {'temp': 1}

class TempClass:
    a = 1
    def temp_function(self):
        pass

print(TempClass.__dict__)
# {'__module__': '__main__', 'a': 1, 'temp_function': <function TempClass.temp_function at 0x0000018FFCA899E0>, '__dict__': <attribute '__dict__' of 'TempClass' objects>, '__weakref__': <attribute '__weakref__' of 'TempClass' objects>, '__doc__': None}
```
>[!error]
> By default, you shouldn't directly access or modify `__dict__`. 
> It's an internal implementation detail and can lead to unexpected behaviour if not used carefully.

^fe593a

- The [[Py vars]] function provides a safer way to get a dictionary view of an object's `__dict__`.
