---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-09-24
---

## `System.Object`
- The base class for all data types (حرفيا كلها)
- This is because C# follows the Object-Oriented Programming (OOP) paradigm, where everything in the language is an object, directly or indirectly deriving from `System.Object`.

- لو عملت function بتاخد object حرفيا تقدر تدخلها أي data type 
  ولو بتـ return object هينفع ترجع أي data type


- All data types **inherits from this class** for 2 reasons:
    - **Generics was invented in 2005** so from 2002 to 2005 System.Object was used for every thing.
    - **set of behaviors should be supported in all Data Types:**
        - Public Virtual String `ToString();` → **return object state (values) in string form**
        - Public Virtual int `GetHashCode();` → **return object identity (unique identifier)**
        - public virtual bool `Equals (Object O2);` → **to check equality**
        - public type `GetType();` → **return data type**

```cs
Object o1; // zero bytes have been allocated in Heap

o1 = new Object();
// new(IL -> newObj)

Object o2 = new Object();
o2 = o1;
```