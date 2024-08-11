---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-05-13
---
The goal of the project is to deploy on your server a simple copy of the [AirBnB website](https://www.airbnb.com/).

After 4 months, you will have a complete web application composed by:

- A command interpreter to manipulate data without a visual interface, like in a Shell (perfect for development and debugging)
- A website (the front-end) that shows the final product to everybody: static and dynamic
- A database or files that store data (data = objects)
- An API that provides a communication interface between the front-end and your data (retrieve, create, delete, update them)

## Final product
![[Pasted image 20240513133651.png]]
![[Pasted image 20240513133657.png]]

## Steps

You won’t build this application all at once, but step by step.

Each step will link to a concept:
### The console
[[AirBnB The Console]]

- create your data model
- manage (create, update, destroy, etc) objects via a console / command interpreter
- store and persist objects to a file ([[JSON]] file)

The first piece is to manipulate a powerful storage system. This storage engine will give us an abstraction between “My object” and “How they are stored and persisted”. This means: from your console code (the command interpreter itself) and from the front-end and RestAPI you will build later, you won’t have to pay attention (take care) of how your objects are stored.

This abstraction will also allow you to change the type of storage easily without updating all of your codebase.

The console will be a tool to validate this storage engine

![[Pasted image 20240513133858.png]]
#### Materials
- [[Py cmd]]
- [[Py UUID]]
- [[Py unittest]]
- [[Py Inheritance]]