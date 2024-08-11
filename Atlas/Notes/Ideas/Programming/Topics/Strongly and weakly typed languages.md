---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-07-09
---
## Strongly Typed
- وانا بعرف ال Variables بتاع لغة البرمجة **بحدد نوعه**
- **Strict rules:** These languages require you to declare the data type (e.g., integer, string) for each variable. The compiler checks these types at compile time and throws errors if you try to use a variable with the wrong type of data.
- **Benefits:**
    - **Fewer runtime errors:** Compile-time checks catch potential issues early, leading to more stable code.
    - **Improved code readability:** Explicit types make code easier to understand for yourself and others.
    - **Potential performance benefits:** The compiler can optimize code based on the known data types.
- **Examples:** Java, [[CSharp MOC|C#]], C++, Pascal
## Weakly Typed
- وانا بعرف ال Variables بتاع لغة البرمجة **مش بحدد نوعه**
- **More flexible:** You don't always need to declare variable types explicitly. The language infers the type based on the value assigned.
- **Benefits:**
    - **Simpler syntax:** Less code to write initially, which can be faster for small programs.
    - **More dynamic:** Easier to change data types on the fly during program execution.
- **Drawbacks:**
    - **More runtime errors:** Type mismatches might not be caught until the program runs, leading to crashes or unexpected behavior.
    - **Potentially less readable code:** Without explicit types, code intent might be less clear.
- **Examples:** [[JavaScript MOC|JS]], [[Python MOC|Python]], PHP, Ruby