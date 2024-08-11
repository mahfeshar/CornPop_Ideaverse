---
up:
  - "[[JavaScript MOC]]"
related:
  - "[[Strings JS]]"
created: 2024-06-30
---
#note/develop🍃 
## JavaScript String Length
```js
let length = text.length;
```

## Extracting String Characters
There are 4 methods for extracting string characters:

- The `at(_position_)` Method
- The `charAt(_position_)` Method
- The `charCodeAt(_position_)` Method
- Using property access [] like in arrays
---
- The `charCodeAt()` method returns the **code of the character** at a specified index in a string (UTF-16 code)
- The `at()` allows the use of **negative indexes** while `charAt()` do not.
  Now you can use `myString.at(-2)` instead of `charAt(myString.length-2)`.
- Property access might be a little **unpredictable:** `text[0]`
	- It makes strings look like arrays (but they are not)
	- If no character is found, [ ] returns undefined, while charAt() returns an empty string.
	- It is read only. str[0] = "A" gives no error (but does not work!)

## Extracting String Parts
There are 3 methods for extracting a part of a string:

- `slice(start, end)`
- `substring(start, end)`
- `substr(start, length)`