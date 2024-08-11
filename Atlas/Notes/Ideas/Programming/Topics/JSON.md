---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-05-07
tags:
  - MOC/DevOps
  - note/develop🍃
Link: https://www.youtube.com/watch?v=iiADhChRriM
---
## Intro to JSON

![[Pasted image 20240427124014.png]]
- JSON: JavaScript Object Notation
- It's data representation format similar to XML or YAML
- It's commonly used for APIs and Configs
- It's used because it's lightweight and easy to Read/Write
- It also integrates very nicely with JavaScript since JSON is just a superset of JavaScript which means every thing you write in JSON is valid JavaScript
- It's integrates Easily with most languages, each language have library or built-in functionality to parse JSON strings into objects or classes in this languages like [[Py json]]

- **Human-readable:** Easy for humans to understand and edit.
- **Language-independent:** Can be used to exchange data between different programming languages.
## JSON types
![[Pasted image 20240427124116.png]]

- Objects like dictionaries, it have key : value (the most used data type)
- Comments are not permitted in JSON
```JSON
{
    "key1": "Value",
    "key2": "Value"
}
```
- You can nest different properties and different types in each other.
- Example: You can put object in object as a value, or you can add array in object

![[Pasted image 20240427124932.png]]
