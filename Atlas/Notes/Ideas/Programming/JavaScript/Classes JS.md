---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-19
---

ECMAScript 2015, also known as ES6, introduced JavaScript Classes.

JavaScript Classes are templates for JavaScript Objects.

## class syntax
```js
class ClassName {
	constructor() { ... }
}
```

```js
class Car {
	constructor(name, year) {
		this.name = name;
		this.year = year;
	}
}
```

The class has two initial properties: "name" and "year".

- A JavaScript class is **not** an object.
- It is a **template** for JavaScript objects.

```js
const myCar1 = new Car("Ford", 2014);
const myCar2 = new Car("Audi", 2019);
```

> [!info]
> The constructor method is called automatically when a new object is created.

## The Constructor Method
The constructor method is a special method:

- It has to have the exact name "constructor"
- It is executed automatically when a new object is created
- It is used to initialize object properties

If you do not define a constructor method, JavaScript will add an empty constructor method.

## Class Methods
Class methods are created with the same syntax as object methods.
```js
class ClassName {  
  constructor() { ... }  
  method_1() { ... }  
  method_2() { ... }  
  method_3() { ... }  
}
```

```js
class Car {
	constructor(name, year) {
		this.name = name;
		this.year = year;
	}
	age() {
		const date = new Date();
		return date.getFullYear() - this.year;
	}
}

const myCar = new Car("Ford", 2014);
documnet.getElementById("demo").innerHTML =
"My car is " + myCar.age() + " years old.";
```

```js
class Car {  
  constructor(name, year) {  
    this.name = name;  
    this.year = year;  
  }  
  age(x) {  
    return x - this.year;  
  }  
}  
  
const date = new Date();  
let year = date.getFullYear();  
  
const myCar = new Car("Ford", 2014);  
document.getElementById("demo").innerHTML=  
"My car is " + myCar.age(year) + " years old.";
```