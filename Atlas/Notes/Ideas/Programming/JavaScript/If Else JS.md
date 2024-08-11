---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-19
---

## Conditional Statements

Very often when you write code, you want to perform different actions for different decisions.

You can use conditional statements in your code to do this.

In JavaScript we have the following conditional statements:

- Use `if` to specify a block of code to be executed, if a specified condition is true
- Use `else` to specify a block of code to be executed, if the same condition is false
- Use `else if` to specify a new condition to test, if the first condition is false
- Use `switch` to specify many alternative blocks of code to be executed

## The if Statement

```js
if (condition) {
	// block of code to be executed if the condition is true_
}

if (_condition_) {  
  //  _block of code to be executed if the condition is true_
} else {  
  //  _block of code to be executed if the condition is false_
}


if (_condition1_) {  
  //  _block of code to be executed if condition1 is true_
} else if (condition2) {  
  //  _block of code to be executed if the condition1 is false and condition2 is true_  
} else {  
  //  _block of code to be executed if the condition1 is false and condition2 is false_
}
```