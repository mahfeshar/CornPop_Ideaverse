---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-07-13
---

Mutable => changeable => [[Py List|Lists]], [[Py Sets|Sets]], [[Py Dictionaries|Dictionaries]] 

Immutable => unchangeable => [[Numbers and operators|Numbers]] (floats, int), [[Py String and text|strings]], [[Py Tuples|Tuples]] and more 

```python
x = 'string'
y = [1, 2]
type(x)
# <class 'str'>
type(y)
<class 'list'>
```
---
The concepts of mutability and immutability refer to whether the state (data) of an object can be changed after it is created.

### Mutable Objects

Mutable objects are those whose state **can be modified** after they are created. 
Most objects in C# are mutable by default.

#### Example of a Mutable Class

```cs
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

class Program
{
    static void Main()
    {
        Person person = new Person { Name = "Alice", Age = 30 };
        Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");

        // Modifying the state of the object
        person.Name = "Bob";
        person.Age = 35;
        Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
    }
}
```

In this example, the `Person` object is mutable because we can change its `Name` and `Age` properties after it is created.

### Immutable Objects

Immutable objects are those whose state **cannot be modified** after they are created. This means once the object is created, it cannot be changed.

#### Example of an Immutable Class

To create an immutable class in C#, follow these guidelines:

1. Mark the class as `sealed` to prevent inheritance (optional but recommended for immutability).
2. Make all fields `readonly`.
3. Initialize all fields via the constructor.
4. Do not provide any methods to modify the fields after initialization.

```cs
public sealed class ImmutablePerson
{
    public string Name { get; }
    public int Age { get; }

    public ImmutablePerson(string name, int age)
    {
        Name = name;
        Age = age;
    }
}

class Program
{
    static void Main()
    {
        ImmutablePerson person = new ImmutablePerson("Alice", 30);
        Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");

        // Attempting to modify the state will result in a compilation error
        
        // person.Name = "Bob"; 
        // Error: Cannot assign to 'Name' because it is read-only
        
        // person.Age = 35;     
        // Error: Cannot assign to 'Age' because it is read-only
    }
}
```

In this example, the `ImmutablePerson` object is immutable because there are **no setters, and its fields can only be set via the constructor**.
Any attempt to modify the properties after creation will result in a compilation error.

### Benefits of Immutability

- **Thread Safety:** Immutable objects are inherently thread-safe as their state cannot change, preventing race conditions.
- **Predictability:** Since their state does not change, immutable objects are easier to reason about and test.
- **Hash Codes:** Immutable objects can be safely used as keys in hash tables since their hash code will not change over time.

### Trade-offs

- **Performance:** Creating new instances for every modification can be less efficient compared to mutating existing instances.
- **Memory Usage:** Immutable objects might use more memory if many intermediate versions of the object are created.

Understanding when to use mutable vs. immutable objects is crucial for designing robust and maintainable software. Mutable objects are flexible and convenient, while immutable objects provide safety and simplicity, especially in concurrent and functional programming contexts.
