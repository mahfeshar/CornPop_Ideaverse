---
up:
  - "[[Py Built in Functions]]"
related: 
created: 2024-04-26
tags:
---
- `type()` returns the object's [[Py class]]. It tells you the exact type an object belongs to.
- This can be helpful in situations where you need to handle different object types differently.
```python
class Animal:
  pass

class Dog(Animal):
  pass

def identify_animal(animal):
  if type(animal) == Dog:
    print(animal, "is a Dog")
  else:
    print(animal, "is not a Dog")

animal = Animal()
dog = Dog()

identify_animal(animal)
# Output: <__main__.Animal object> is not a Dog
identify_animal(dog)
# Output: <__main__.Dog object> is a Dog
```