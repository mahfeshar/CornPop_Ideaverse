---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-18
---

JavaScript Variables can be declared in 4 ways:

- Automatically
- Using `var`
- Using `let`
- Using `const`

| Keyword | Description               |
| ------- | ------------------------- |
| var     | Declares a variable       |
| let     | Declares a block variable |
| const   | Declares a block constant |

> [!notes]
> It is considered good programming practice to always declare variables before use.

We can automatically declare the varibles
```js
x = 5; 
y = 6;
z = 5 + 6;
```

We can declare it.
```js
var x = 5;  
var y = 6;  
var z = x + y;
```

> [!info]
> The `var` keyword should only be used in code written for older browsers.


```js
const x = 5;  
const y = 6;  
const z = x + y;
```

## One Statement, Many Variables
```js
let person = "John Doe", carName = "Volvo", price = 200;
```

A declaration can span multiple lines:
```js
let person = "John Doe",  
carName = "Volvo",  
price = 200;
```

## Value = undefined
A variable declared without a value will have the value `undefined`.
The value can be something that has to be calculated, or something that will be provided later, like user input.
```js
let carName;
```

> [!error]
> You cannot re-declare a variable declared with `let` or `const`.
> This will not work:
> ```js
let carName = "Volvo";  
let carName;
>```

## Some Arithmetuc
You can also add strings, but strings will be concatenated:
```js
let x = "John" + " " + "Doe";

let x = "5" + 2 + 3; // 523 : string

let x = 2 + 3 + "5"; // 55
```

## Dollar Sign $
Since JavaScript treats a dollar sign as a letter, identifiers containing $ are valid variable names:

```js
let $ = "Hello World";  
let $$$ = 2;  
let $myMoney = 5;
```

Using the dollar sign is not very common in JavaScript, but professional programmers often use it as an alias for the main function in a JavaScript library.

In the JavaScript library jQuery, for instance, the main function `$` is used to select HTML elements. In jQuery `$("p");` means "select all p elements".

## Underscore (\_)
Since JavaScript treats underscore as a letter, identifiers containing _ are valid variable names:
```js
let _lastName = "Corn";
let _x = 2;  
let _100 = 5;
```

Using the underscore is not very common in JavaScript, but a convention among professional programmers is to use it as an alias for "private (hidden)" variables.