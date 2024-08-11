---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-18
---

- Variables defined with `const` cannot be **Redeclared**

- Variables defined with `const` cannot be **Reassigned**

- Variables defined with `const` have **Block Scope**

## Cannot be Reassigned
```js
const PI = 3.141592653589793;  
PI = 3.14;      // This will give an error  
PI = PI + 10;   // This will also give an error
```

## Must be Assigned

```js
const PI = 3.14159265359;


//Error
const PI;  
PI = 3.14159265359;
```

## When to use JavaScript const?

**Always declare a variable with `const` when you know that the value should not be changed.**

Use `const` when you declare:

- A new Array
- A new [[Objects JS]]
- A new [[Functions JS]]
- A new RegExp

## Constant Objects and Arrays

The keyword `const` is a little misleading.

It does not define a constant value. It defines a constant reference to a value.

Because of this you can NOT:

- Reassign a constant value
- Reassign a constant array
- Reassign a constant object

But you CAN:

- Change the elements of constant array
- Change the properties of constant object

## Constant Arrays
```js
// You can create a constant array:  
const cars = ["Saab", "Volvo", "BMW"];  
  
// You can change an element:  
cars[0] = "Toyota";  
  
// You can add an element:  
cars.push("Audi");


// Error
const cars = ["Saab", "Volvo", "BMW"];  
  
cars = ["Toyota", "Volvo", "Audi"];    // ERROR
```

## Constant Objects
```js
// You can create a const object:  
const car = {type:"Fiat", model:"500", color:"white"};  
  
// You can change a property:  
car.color = "red";  
  
// You can add a property:  
car.owner = "Johnson";

// Error
const car = {type:"Fiat", model:"500", color:"white"};  
  
car = {type:"Volvo", model:"EX60", color:"red"};    // ERROR
```

## Block Scope

Declaring a variable with `const` is similar to `let` when it comes to **Block Scope**.

```js
const x = 10;  
// Here x is 10  
  
{  
const x = 2;  
// Here x is 2  
}  
  
// Here x is 10
```

## Redeclaring

```js
var x = 2;     // Allowed  
const x = 2;   // Not allowed  
  
{  
let x = 2;     // Allowed  
const x = 2;   // Not allowed  
}  
  
{  
const x = 2;   // Allowed  
const x = 2;   // Not allowed  
}
```

## Hoisting

Variables defined with `var` are **hoisted** to the top and can be initialized at any time.

Variables defined with `const` are also hoisted to the top, but not initialized.

```js
alert (carName);  
const carName = "Volvo";
```