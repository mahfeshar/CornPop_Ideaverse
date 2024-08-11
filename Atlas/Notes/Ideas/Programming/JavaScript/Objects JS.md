---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-30
---

We talked about it object at [[Data Types JS#The Object Datatype]]

# Intro

![[Pasted image 20240630124155.png]]

## Properties 
في مثال العربية دا مثلًا بنقول إن العربية نوعها فيات ولونها أبيض ووزنها 850 وهكذا
فهي خصائص ال object
Car objects have the same **properties**, but the **values** differ from car to car.
يعني كل العربيات بيبقا ليها لون وليها وزن وهكذا بس القيم بتختلف فممكن واحدة لونها يبقا أحمر

## Methods
ف نفس مثال العربية فالعربية ممكن تمشي وتقف أو تفرمل وهكذا 
فهي الطرق أو الأفعال اللي ممكن العربية تعملها
Car objects have the same **properties**, but the **values** differ from car to car.
ممكن كل عربية تنفذ الmethods دي في طرق مختلفة

## Variables
JavaScript variables are containers for data values.
This code assigns a **simple value** (Fiat) to a **variable** named car:

```js
let car = "Fiat";
```

## Objects 
هي عبارة عن Variables بس ممكن يبقا فيها أكتر من value
```js
const car = {type:"Fiat", model:"500", color:"white"};
```

> [!info]
> It is a common practice to declare objects with the const keyword. [[const JS]]

# Objects

## Define Object
How to Define a JavaScript Object
- Using an Object Literal
- Using the `new` Keyword
- Using an Object Constructor

### JavaScript Object Literal
An object literal is a list of **name:value** pairs inside curly braces **{}**.

`{firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"}`

#### Note:
- **name:value pairs** are also called **key:value pairs**.
- **object literals** are also called **object initializers**.

### Creating a JavaScript Object
```js
// Create an Object  
const person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};

// Empty object
const person = {};
person.firstname = "Corn";
person.lastName = "Doe";  
person.age = 50;  
person.eyeColor = "blue";
```

### Using the new Keyword

```js
// Create an Object  
const person = new Object();  
  
// Add Properties  
person.firstName = "John";  
person.lastName = "Doe";  
person.age = 50;  
person.eyeColor = "blue";
```

مش بيبقا أحسن حاجة إننا نستخدم كلمة new والأفضل اننا نستخدم ال object literal عشان السرعة والقراءة والبساطة

## Object Properties
- The **named values**, in JavaScript objects, are called **properties**.
- Properties are the most important part of JavaScript objects.
- Properties can be changed, added, deleted, and some are read only.
---
Objects written as name value pairs are similar to:

- Associative arrays in PHP
- Dictionaries in Python [[Py dictionary]]
- Hash tables in C
- Hash maps in Java
- Hashes in Ruby and Perl
### Accessing Object Properties
```js
// Two ways:
objectName.propertName // person.lastName;
objectName["propertyName"] // person["lastName"];
```

### Adding New Properties
```js
person.country = "Egypt";
```

### Delete Properties
The `delete` keyword deletes a property from an object:
```js
delete person.age;
delete person["age"];
```

### Nested Objects
```js
myObj = {
	name:"Corn",
	age:30,  
	myCars: {  
	    car1:"Ford",  
	    car2:"BMW",  
	    car3:"Fiat"  
	}
}

myObj.myCars.car2;
myObj.myCars["car2"];
myObj["myCars"]["car2"];
```
## Object Methods
- Methods are **actions** that can be performed on objects.
- Methods are [[Functions JS|function]] **definitions** stored as **property values**.

```js
const person = {  
  firstName: "John",  
  lastName : "Doe",  
  id       : 5566,  
  fullName : function() {  
    return this.firstName + " " + this.lastName;  
  }  
};
```

In the example above, `this` refers to the **person object**:
**this.firstName** means the **firstName** property of **person**.

### Accessing Object Methods
```js
objectName.methodName()

name = person.fullName();
name = person.fullName; // It will return the function definition
```
### Adding a Method
```js
person.name = function () {  
	return this.firstName + " " + this.lastName;  
};
```
## In JavaScript, Objects are King.
If you Understand Objects, you Understand JavaScript.

> **Objects** are containers for **Properties** and **Methods**.
> **Properties** are named **Values**.
> **Methods** are **Functions** stored as **Properties**.
> **Properties** can be primitive values, functions, or even other objects.

In JavaScript, almost "everything" is an object.

- Objects are objects
- Maths are objects
- Functions are objects
- Dates are objects
- Arrays are objects
- Maps are objects
- Sets are objects

All JavaScript values, except primitives, are objects. [[Data Types JS#JavaScript Primitives|Primitives]]

And we said before that Primitives are immutable but:
### Objects are Mutable
Objects are mutable: They are addressed by reference, not by value.
If person is an object, the following statement will not create a copy of person:
```js
const x = person; // Same person
```

The object x is **not a copy** of person. The object x **is** person.

The object x and the object person share the same memory address.

Any changes to x will also change person:

```js
const person = {
	firstName: "John",
	lastName: "Doe",
	age: 50,
	eyeColor: "blue"
}

const x = person;

x.age = 10; // Changed in both
```

## Display Objects

لو جربت تعرض ال object عادي مش هيعرضه انما هيقول نوعه بس
Displaying a JavaScript object will output **\[object Object]**.
```js
// Create an Object  
const person = {  
  name: "John",  
  age: 30,  
  city: "New York"  
};  
  
document.getElementById("demo").innerHTML = person; // [object Object]
```

Some solutions to display JavaScript objects are:

- Displaying the Object Properties by name
- Displaying the Object Properties in a Loop
- Displaying the Object using Object.values()
- Displaying the Object using JSON.stringify()

### Displaying the Object Properties by name
```js
// Create an Object  
const person = {  
  name: "John",  
  age: 30,  
  city: "New York"  
};  
  
// Display Properties  
document.getElementById("demo").innerHTML =  
person.name + "," + person.age + "," + person.city; 
// John, 30, New York
```

### Displaying the Object Properties in a Loop
```js
const person = {
	name: "Corn",
	age: 30,
	city: "Tanta"
};

let text = "";

for (let x in person) {
	text += person[x] + " ";
};

// Display the Text  
document.getElementById("demo").innerHTML = text;
// John 30 New York
```

#### Note:
You must use **person\[x]** in the loop.
**person.x** will not work (Because **x** is the loop variable).

### Using Object.values()
Creates an [[Array JS]] from the property **values**

```js
const person = {
	name: "Corn",
	age: 30,
	city: "Tanta"
};

const myArray = Object.values(person);

document.getElementById("demo").innerHTML = myArray;
```

### Using Object.entries()
makes it simple to use objects in loops:

```js
const fruits = {Bananas:300, Oranges:200, Apples:500};

let text = "";
for (let [fruit, value] of Object.entires(fruites)) {
	text += fruit + ": " + value + "<br>";
}
```

### Using JSON.stringify()
JavaScript objects can be converted to a string with [[JSON]] method `JSON.stringify()`.
The result will be a string written in JSON notation:
`{"name":"John","age":50,"city":"New York"}`

```js
// Create an Object  
const person = {  
  name: "John",  
  age: 30,  
  city: "New York"  
};  
  
// Stringify Object  
let myString = JSON.stringify(person);  
  
// Display String  
document.getElementById("demo").innerHTML = myString;
// {"name":"John","age":30,"city":"New York"}
```

