---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-18
---

- Variables declared with `let` have **Block Scope**

- Variables declared with `let` must be **Declared** before use

- Variables declared with `let` cannot be **Redeclared** in the same scope

```js
{  
  let x = 2;  
}  
// x can NOT be used here
```

## Global Scope
Variables declared with the `var` always have **Global Scope**.

```js
{  
  var x = 2;  
}  
// x CAN be used here
```

## Cannot be Redeclared

Variables defined with `let` **can not** be redeclared.
Variables defined with `var` **can** be redeclared.
```js
let x = "John Doe";  
let x = 0; // Error

var x = "John Doe";  
var x = 0; // OK
```

Redeclaring a variable using the `var` keyword can impose problems.
Redeclaring a variable inside a block will also redeclare the variable outside the block.

But
With `let` we can redeclare variable and Redeclaring a variable inside a block will not redeclare the variable outside the block

## Difference Between var, let and const

|       | Scope | Redeclare | Reassign | Hoisted | Binds this |
| ----- | ----- | --------- | -------- | ------- | ---------- |
| var   | No    | Yes       | Yes      | Yes     | Yes        |
| let   | Yes   | No        | Yes      | No      | No         |
| const | Yes   | No        | No       | No      | No         |

### What is Good?

`let` and `const` have **block scope**.

`let` and `const` can not be **redeclared**.

`let` and `const` must be **declared** before use.

`let` and `const` does **not bind** to `this`.

`let` and `const` are **not hoisted**.

### What is Not Good?

`var` does not have to be declared.

`var` is hoisted مرفوع.

`var` binds to this.

## Redeclaring
Redeclaring a JavaScript variable with `var` is allowed anywhere in a program:
```js
var x = 2
// Now x = 2

var x = 3;
// Now x is 3
```


With `let`, redeclaring a variable in the same block is NOT allowed:

```js
var x = 2;   // Allowed  
let x = 3;   // Not allowed  
  
{  
let x = 2;   // Allowed  
let x = 3;   // Not allowed  
}  
  
{  
let x = 2;   // Allowed  
var x = 3;   // Not allowed  
}
```

Redeclaring a variable with `let`, in another block, IS allowed:
```js
let x = 2;   // Allowed  
  
{  
let x = 3;   // Allowed  
}  
  
{  
let x = 4;    // Allowed  
}
```

## Let Hoisting

Variables defined with `var` are **hoisted** to the top and can be initialized at any time.

Meaning: You can use the variable before it is declared:

```js
carName = "Volvo";  
var carName;
```

Variables defined with `let` are also hoisted to the top of the block, but not initialized.

Meaning: Using a `let` variable before it is declared will result in a `ReferenceError`:

```js
carName = "Saab";  
let carName = "Volvo"; // Error
```