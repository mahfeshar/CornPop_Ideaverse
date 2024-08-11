---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-30
---

- Strings are for **storing text**
- Strings are written **with quotes**
---
- A JavaScript string is zero or more characters written inside quotes.
```js
let carName1 = "Volvo XC60";  // Double quotes  
let carName2 = 'Volvo XC60';  // Single quotes
```

- تقدر تستخدم جوا ال string ال quotes نفسها بشرط ان اللي برا ميبقاش زي اللي جوا
```js
let answer1 = "It's alright";  
let answer2 = "He is called 'Johnny'";  
let answer3 = 'He is called "Johnny"';
```

## Template Strings
- Templates were introduced with ES6 (JavaScript 2016).
- Templates are strings enclosed in backticks (`This is a template string`).
- Templates allow single and double quotes inside a string:
```js
let text = `He's often called "Johnny"`;
```

- Templates allow multiline strings:
```js
let text =  
`The quick  
brown fox  
jumps over  
the lazy dog`;
```
## String Length

```js
let text = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
let length = text.length;
```

## Escape Characters
The backslash escape character (`\`) turns special characters into string characters:

| Code | Result         | Description  |
| ---- | -------------- | ------------ |
| `\'` | '              | Single quote |
| `\"` | "              | Double quote |
| `\\` | `\`|Backslash |

| Code | Result               |
| ---- | -------------------- |
| \b   | Backspace            |
| \f   | Form Feed            |
| \n   | New Line             |
| \r   | Carriage Return      |
| \t   | Horizontal Tabulator |
| \v   | Vertical Tabulator   |
The 6 escape characters above were originally designed to control typewriters, teletypes, and fax machines. **They do not make any sense in HTML**.

## Breaking Long Lines
For readability, programmers often like to avoid long code lines.
A safe way to break up a **statement** is after an operator:
```js
document.getElementById("demo").innerHTML =  
"Hello Dolly!";

document.getElementById("demo").innerHTML = "Hello " +  
"Dolly!";
```

## JavaScript Strings as Objects
Normally, JavaScript strings are primitive values, created from literals:
```js
let x = "John";
```

But strings can also be defined as objects with the keyword `new`:
```js
let y = new String("John");
```

> Do not create Strings objects.
> The `new` keyword complicates the code and slows down execution speed.
> String objects can produce unexpected results:

When using the `\==` operator, x and y are **equal**

```js
let x = "John";  
let y = new String("John");
```

When using the `\===` operator, x and y are **not equal**:

```js
let x = "John";  
let y = new String("John");
```

>Note the difference between `(x==y)` and `(x===y)`.

