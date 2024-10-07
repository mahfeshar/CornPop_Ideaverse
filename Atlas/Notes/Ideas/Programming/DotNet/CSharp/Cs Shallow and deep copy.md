---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-07
---

## Shallow and deep copy
- We talked about this before [[Py Shallow and Deep copy]]
#### Shallow Copy
![[Pasted image 20241007043103.png]]

A shallow copy of an object copies **the references of nested objects**, not the actual nested objects themselves. 
This means that changes made to the nested objects in the copied array or object will reflect in the original array or object and vice versa.
We can make it with [[Cs Arrays#Array copy|copy]]
#### Deep Copy

A deep copy of an object copies not only the object itself **but also the objects that are referenced by the original object**. 
This means that changes made to the nested objects in the copied array or object will not affect the original array or object and vice versa.

#### Example in C\#

Consider the following example:

```cs
using System;

class Person
{
    public string Name { get; set; }
}

class Program
{
    static void Main()
    {
        // Create an array of Person objects
        Person[] originalArray = new Person[2];
        originalArray[0] = new Person { Name = "Alice" };
        originalArray[1] = new Person { Name = "Bob" };

        // Shallow copy
        Person[] shallowCopyArray = new Person[originalArray.Length];
        Array.Copy(originalArray, shallowCopyArray, originalArray.Length);

        // Deep copy
        Person[] deepCopyArray = new Person[originalArray.Length];
        for (int i = 0; i < originalArray.Length; i++)
        {
            deepCopyArray[i] = new Person { Name = originalArray[i].Name };
        }

        // Change the name of the first person in the shallow copy
        shallowCopyArray[0].Name = "Charlie";

        // Change the name of the second person in the deep copy
        deepCopyArray[1].Name = "Dave";

        // Display the names in the original array
        Console.WriteLine("Original Array:");
        foreach (var person in originalArray)
        {
            Console.WriteLine(person.Name);
        }

        // Display the names in the shallow copy array
        Console.WriteLine("\nShallow Copy Array:");
        foreach (var person in shallowCopyArray)
        {
            Console.WriteLine(person.Name);
        }

        // Display the names in the deep copy array
        Console.WriteLine("\nDeep Copy Array:");
        foreach (var person in deepCopyArray)
        {
            Console.WriteLine(person.Name);
        }
    }
}

```
#### Explanation

1. **Original Array**:
    - Contains two `Person` objects: "Alice" and "Bob".
2. **Shallow Copy**:
    - Uses `Array.Copy` to create a new array `shallowCopyArray` that references the same `Person` objects as the `originalArray`.
3. **Deep Copy**:
    - Manually creates a new array `deepCopyArray` and new `Person` objects with the same names as those in the `originalArray`.
4. **Modifications**:
    - Changing the name of the first person in `shallowCopyArray` to "Charlie" affects the `originalArray` because they reference the same objects.
    - Changing the name of the second person in `deepCopyArray` to "Dave" does not affect the `originalArray` because they are separate objects.

#### Output
```plaintext
Original Array:
Charlie
Bob

Shallow Copy Array:
Charlie
Bob

Deep Copy Array:
Alice
Dave
```

As shown, the shallow copy reflects changes in the original array, while the deep copy does not. This illustrates the fundamental difference between shallow and deep copying in C#.