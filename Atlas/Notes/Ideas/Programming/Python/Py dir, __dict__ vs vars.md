---
up:
  - "[[Python MOC]]"
related:
  - "[[Py dir]]"
  - "[[Py __dict__]]"
  - "[[Py vars]]"
created: 2024-04-29
tags:
  - note/develop🍃
---

| Feature              | dir(obj)                          | obj.**dict**                   | vars(obj)                                       |
| -------------------- | --------------------------------- | ------------------------------ | ----------------------------------------------- |
| Scope                | Object, class, and ancestors      | Object's instance attributes   | Object's instance attributes                    |
| Output format        | List of strings (attribute names) | Dictionary                     | Dictionary                                      |
| Modifying attributes | Not recommended                   | Possible, but use with caution | Possible, but use with caution<br><br>pen_spark |

## **1. Scope:**
- `dir(obj)`: This function returns a list containing the names of all attributes (_including methods_) of the object (`obj`), its class, and even attributes inherited from ancestor classes. It gives a broader view.
- `obj.__dict__`: This is a direct reference to the dictionary storing the instance attributes (data attributes, _not methods_) of the specific object (`obj`). It only shows what's defined directly on that object.
- `vars(obj)`: This function is similar to `obj.__dict__`. It returns a dictionary representing the object's symbol table, which is essentially the same as the `__dict__` attribute.
## **2. Output format:**
- `dir(obj)`: Returns a sorted [[Py list]] of strings (attribute names).
- `obj.__dict__` and `vars(obj)`: Both return an actual [[Py dictionary]] object. You can access attribute values using their keys in this dictionary.
## **3. Modifying attributes:**
- While you can modify attribute values through both `obj.__dict__` and the dictionary returned by `vars(obj)`, it's generally recommended to use the object's attribute access syntax (`obj.attribute_name`) for clarity and potential method behavior.

## **In essence:**

- Use `dir(obj)` when you want to explore all possible attributes (including methods) an object might have.
- Use `obj.__dict__` or `vars(obj)` when you specifically need to access or modify an object's instance attributes as a dictionary.
## Example
```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def say_hi(self):
    print("Hi, my name is", self.name)

person1 = Person("Alice", 30)

# Using dir()
print("Attributes using dir():")
print(dir(person1))  # This will include methods like say_hi

# Using __dict__
print("\nInstance attributes using __dict__:")
print(person1.__dict__)  # Only instance attributes (name, age)

# Using vars()
print("\nInstance attributes using vars():")
print(vars(person1))  # Same output as __dict__

```
This code defines a `Person` class with `name` and `age` attributes and a `say_hi` method. We then create an instance `person1`.

- `dir(person1)` shows a list of all attributes, including methods inherited from the class and even built-in methods like `__init__`.
- `person1.__dict__` and `vars(person1)` both show a dictionary containing only the instance attributes (`name` and `age`) defined directly on `person1`.

Remember, modifying attributes through the dictionary is possible, but for clarity and potential method behaviour, using `person1.name` or `person1.age` is generally preferred.
