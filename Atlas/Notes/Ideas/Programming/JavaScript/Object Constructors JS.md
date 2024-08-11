---
up:
  - "[[JavaScript MOC]]"
related:
  - "[[Objects JS]]"
created: 2024-06-30
---

## Intro
- بعض الأحيان بنبقا عايزين نعمل أكتر من object بنفس النوع type
- To create an **object type** we use an **object constructor function**.
- It is considered good practice to name constructor functions with an upper-case first letter.

```js
function Person(first, last, age, eye) {
	this.firstName = first;
	this.lastName = last;
	this.age = age;
	this.eyeColoe = eye;
}

const myFather = new Person("John", "Doe", 50, "blue");
const myMother = new Person("Sally", "Rally", 48, "green");
const mySister = new Person("Anna", "Rally", 18, "green");
const mySelf = new Person("Johnny", "Rally", 22, "green");
```

### Note:
In the constructor function, `this` has no value.
The value of `this` will become the new object when a new object is created.

## Property
### Property Default Values
A **value** given to a property will be a **default value** for all objects created by the constructor:
```js
function Person(first, last, age, eyecolor) {  
  this.firstName = first;  
  this.lastName = last;  
  this.age = age;  
  this.eyeColor = eyecolor;  
  this.nationality = "English";  
}
```

### Adding a Property to an Object
Adding a property to a created object is easy:
```js
myFather.nationality = "English";
```

The property will be added to **myFather**. Not to any other **Person Objects**.

### Adding a Property to a Constructor
You can **NOT** add a new property to an object constructor:
```js
Person.nationality = "English";
```
دا ال constructor نفسه فلو جيت أستخدم أي Object منه مش هيظهر حاجة ومش هياخدها

To add a new property, you must add it to the constructor function prototype:
```js
Person.prototype.nationality = "English";
```


## Methods

```js
function Person(first, last, age, eyecolor) {  
  this.firstName = first;  
  this.lastName = last;  
  this.age = age;  
  this.eyeColor = eyecolor;  
  this.fullName = function() {  
    return this.firstName + " " + this.lastName;  
  };  
}
```

### Adding a Method to an Object
```js
myMother.changeName = function (name) {  
  this.lastName = name;  
}
```

The method will be added to **myFather**. Not to any other **Person Objects**.

### Adding a Method to a Constructor
You cannot add a new method to an object constructor function.
```js
Person.changeName = function (name) {  
  this.lastName = name;  
}  
  
myMother.changeName("Doe");
```

> [!error]
> This code will produce a TypeError

Adding a new method must be done to the constructor function prototype:

```js
Person.prototype.changeName = function (name) {  
  this.lastName = name;  
}  
  
myMother.changeName("Doe");
```

## Built-in JavaScript Constructors
```js
new Object()   // A new Object object  
new Array()    // A new Array object  
new Map()      // A new Map object  
new Set()      // A new Set object  
new Date()     // A new Date object  
new RegExp()   // A new RegExp object  
new Function() // A new Function object
```

The `Math()` object is not in the list. `Math` is a global object. The `new` keyword cannot be used on `Math`.

### Also 
Use object literals `{}` instead of `new Object()`.

Use array literals `[]` instead of `new Array()`.

Use pattern literals `/()/` instead of `new RegExp()`.

Use function expressions `() {}` instead of `new Function()`.

```js
"";           // primitive string  
0;            // primitive number  
false;        // primitive boolean  
  
{};           // object object  
[];           // array object  
/()/          // regexp object  
function(){}; // function
```