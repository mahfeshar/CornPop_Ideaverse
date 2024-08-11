---
up:
  - "[[Py Built in Functions]]"
related: 
created: 2024-05-07
tags: []
---

- It checks if the first class argument is a subclass of the second class argument.
- This can be helpful for checking if a class inherits from a specific base class at [[Py Inheritance]]
```python
class Animal:
  pass

class Dog(Animal):
  pass

print(issubclass(Dog, Animal))  
# Output: True (Dog is a subclass of Animal)
print(issubclass(Animal, Dog))  
# Output: False (Animal is not a subclass of Dog)
```