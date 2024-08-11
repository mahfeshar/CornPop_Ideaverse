---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-18
---

## JavaScript Primitives
- Primitives are values that have no properties or methods
عندنا 5 أنواع:

![[Pasted image 20240624053359.png]]
- symbol
- bigint
- ملهومش properties or methods
- أي حاجة غيرهم هي عبارة عن Object

### Immutable
Primitive values are immutable (they are hardcoded and cannot be changed).
if x = 3.14, you can change the value of x, but you cannot change the value of 3.14.

| Value     | Type          | Comment                       |
| --------- | ------------- | ----------------------------- |
| "Hello"   | string        | "Hello" is always "Hello"     |
| 3.14      | number        | 3.14 is always 3.14           |
| true      | boolean       | true is always true           |
| false     | boolean       | false is always false         |
| null      | null (object) | null is always null           |
| undefined | undefined     | undefined is always undefined |
### Wrapper Objects

- عاملة زي غلاف للعناصر اللي فوق اللي قولنا ملهاش methods انما دي بيبقا فيها special methods
- بيبقا ليها نفس الإسم بتاع ال primitive بس بيبدأ بحرف كابتل 
- اللغة JS بتديك صلاحية انك تحول بين wrapper objects و primitive values
- عشان نعمل wrapper object جديد بنستخدم `new` ونقدر نحول الobject دا ل primitive عن طريق `valueOf()`

![[Pasted image 20240624053800.png]]
![[Pasted image 20240624053953.png]]
## JavaScript has 8 Datatypes

String  
Number  
Bigint  
Boolean  
Undefined  
Null  
Symbol  
Object

## The Object Datatype

The object data type can contain both **built-in objects**, and **user defined objects**:

Built-in object types can be:

objects, arrays, dates, maps, sets, intarrays, floatarrays, promises, and more.

```js
// Numbers:  
let length = 16;  
let weight = 7.5;  
  
// Strings:  
let color = "Yellow";  
let lastName = "Johnson";  
  
// Booleans  
let x = true;  
let y = false;  
  
// Object:  
const person = {firstName:"John", lastName:"Doe"};  
  
// Array object:  
const cars = ["Saab", "Volvo", "BMW"];  
  
// Date object:  
const date = new Date("2022-03-25");
```