---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-18
---

- A JavaScript function is a block of code designed to perform a particular task.
- A JavaScript function is executed when "something" invokes it (calls it).

```js
// Function to compute the product of p1 and p2  
function myFunction(p1, p2) {  
  return p1 * p2;  
}
```

## Syntax
```js
function name(parameter1, parameter2, parameter3) {  
  // code to be executed  
}
```

## Function Invocation

The code inside the function will execute when "something" **invokes** (calls) the function:

- When an event occurs (when a user clicks a button)
- When it is invoked (called) from JavaScript code
- Automatically (self invoked)

## Function Return

When JavaScript reaches a `return` statement, the function will stop executing.

```js
// Function is called, the return value will end up in x  
let x = myFunction(4, 3);  
  
function myFunction(a, b) {  
// Function returns the product of a and b  
  return a * b;  
}
```

## The ( ) Operator
دا عشان أنادي على ال function
```js
function toCelsius(fahrenheit) {
	return (5/9) * (fahrenheit-32)
}

let value = toCelsius(77);
let value = toCelsius(); // Will return wrong answer: NaN
let value = toCelsius; // return the function and not result
```

As you see from the examples above, `toCelsius` refers to the function object, and `toCelsius()` refers to the function result.

## Local Variables
Variables declared within a JavaScript function, become **LOCAL** to the function.
Local variables can only be accessed from within the function.

```js
// code here can NOT use carName  
  
function myFunction() {  
  let carName = "Volvo";  
  // code here CAN use carName  
}  
  
// code here can NOT use carName
```