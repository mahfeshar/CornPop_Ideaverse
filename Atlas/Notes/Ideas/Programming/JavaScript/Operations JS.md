---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-18
---

## Arithmetic Operators
| Operator | Description                                                         |
| -------- | ------------------------------------------------------------------- |
| +        | Addition                                                            |
| -        | Subtraction                                                         |
| *        | Multiplication                                                      |
| **       | Exponentiation ([ES2016](https://www.w3schools.com/js/js_2016.asp)) |
| /        | Division                                                            |
| %        | Modulus (Division Remainder)                                        |
| ++       | Increment                                                           |
| --       | Decrement                                                           |

## Assignment Operators

| Operator | Example | Same As    |
| -------- | ------- | ---------- |
| =        | x = y   | x = y      |
| +=       | x += y  | x = x + y  |
| -=       | x -= y  | x = x - y  |
| *=       | x *= y  | x = x * y  |
| /=       | x /= y  | x = x / y  |
| %=       | x %= y  | x = x % y  |
| \*\*=    | x **= y | x = x ** y |

## Comparison Operators

| Operator | Description                       |
| -------- | --------------------------------- |
| ==       | equal to                          |
| ===      | equal value and equal type        |
| !=       | not equal                         |
| !==      | not equal value or not equal type |
| >        | greater than                      |
| <        | less than                         |
| >=       | greater than or equal to          |
| <=       | less than or equal to             |
| ?        | ternary operator                  |

## String Addition
```js
let text1 = "John";  
let text2 = "Doe";  
let text3 = text1 + " " + text2;

let text1 = "What a very ";  
text1 += "nice day";
// What a very nice day
```

## Adding Strings and Numbers
```js
let x = 5 + 5;  
let y = "5" + 5;  
let z = "Hello" + 5;
/*
10  
55  
Hello5
*/
```

## Logical Operators
| Operator | Description |
| -------- | ----------- |
| &&       | logical and |
| \|       | logical or  |
| !        | logical not |
## Type Operators
| Operator   | Description                                                |
| ---------- | ---------------------------------------------------------- |
| typeof     | Returns the type of a variable                             |
| instanceof | Returns true if an object is an instance of an object type |

## Bitwise Operators

Bit operators work on 32 bits numbers.

| Operator | Description          | Example | Same as      | Result | Decimal |
| -------- | -------------------- | ------- | ------------ | ------ | ------- |
| &        | AND                  | 5 & 1   | 0101 & 0001  | 0001   | 1       |
| \|       | OR                   | 5 \| 1  | 0101 \| 0001 | 0101   | 5       |
| ~        | NOT                  | ~ 5     | ~0101        | 1010   | 10      |
| ^        | XOR                  | 5 ^ 1   | 0101 ^ 0001  | 0100   | 4       |
| <<       | left shift           | 5 << 1  | 0101 << 1    | 1010   | 10      |
| >>       | right shift          | 5 >> 1  | 0101 >> 1    | 0010   | 2       |
| >>>      | unsigned right shift | 5 >>> 1 | 0101 >>> 1   | 0010   | 2       |

The examples above uses 4 bits unsigned examples. But JavaScript uses 32-bit signed numbers.  
Because of this, in JavaScript, ~ 5 will not return 10. It will return -6.  
~00000000000000000000000000000101 will return 11111111111111111111111111111010


## Assignment
### The <<= Operator
The **Left Shift Assignment Operator** left shifts a variable.
```js
let x = -100;
x <<= 5; // -3200
```
### The >>= Operator
The **Right Shift Assignment Operator** right shifts a variable (signed).
```js
let x = -100;  
x >>= 5; // -4
```

### The >>>= Operator
The **Unsigned Right Shift Assignment Operator** right shifts a variable (unsigned).
```js
let x = -100;  
x >>>= 5; // 134217724
```

### The &&= Operator
The **Logical AND assignment operator** is used between two values.
If the first value is true, the second value is assigned.
```js
let x = 10;  
x &&= 5; // 5
```
### The ||= Operator
The **Logical OR assignment operator** is used between two values.
If the first value is false, the second value is assigned.
```js
let x = 10;  
x ||= 5; // 5
```
### The ??= Operator
The **Nullish coalescing assignment operator** is used between two values.
If the first value is undefined or null, the second value is assigned.
```js
let x;  
x ??= 5; // 5
```