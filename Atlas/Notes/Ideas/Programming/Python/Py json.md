---
up:
  - "[[Py Module]]"
related:
  - "[[JSON]]"
created: 2024-04-27
tags:
---
- We explained [[JSON]] before.
- Python has a built-in package called `json`, which can be used to work with JSON data.
- We should import it first `import json`
- It's look like [[Py dictionary]]
## Serialization and Deserialization
### Serialization
Serialization refers to the process of converting an in-memory object (like a dictionary, list, custom class instance, etc.) into a format that can be:
- **Stored:** Saved to a file (like `.txt`, `.dat`, `.json`) or a database for later use.
- **Transmitted:** Sent across a network (e.g., between servers, to a client) for communication.
### Deserialization
Deserialization is the reverse process of serialization. It takes the serialized data (the byte stream, JSON string, or other format) and converts it back into its original object form in memory, ready to be used again by your program.
## From Python to JSON (Serialization)
- We will use `json.dumps`
```python
import json

# a Python object (dict):  
x = {  
    "name": "John",  
    "age": 30,  
    "city": "New York"  
}

y = json.dumps(x)
print(y) # JSON string
```
### Legal data types

| Python | JSON   |
| ------ | ------ |
| dict   | Object |
| list   | Array  |
| tuple  | Array  |
| str    | String |
| int    | Number |
| float  | Number |
| True   | true   |
| False  | false  |
| None   | null   |
```python
import json  
  
x = {  
  "name": "John",  
  "age": 30,  
  "married": True,  
  "divorced": False,  
  "children": ("Ann","Billy"),  
  "pets": None,  
  "cars": [  
    {"model": "BMW 230", "mpg": 27.5},  
    {"model": "Ford Edge", "mpg": 24.1}  
  ]  
}  
  
print(json.dumps(x))
```
### Format the Result
- We will use `indent` with `dumps` to make it easier to read the result
```python
json.dumps(x, indent=4) # number of spaces 4
```
- Use the `separators` parameter to change the default separator
```python
json.dumps(x, indent=4, separators=(". ", " = "))
```
- We can order the keys with `sort_keys`
```python
json.dumps(x, indent=4, sort_keys=True)
```
## From JSON to Python (Deserialization)
- We will use `json.loads()` - **don't forget s for string not file**
- The result will be a [[Py dictionary]]
```python
import json

# JSON
x = '{"name": "Corn", "age":30, "city":"Mahalla"}'

y = json.loads(x) # dictionary
print(y["age"])
```
## With files
- We can use `JSON` [[Py File Handling|files]] to read data from it and write data and so on.
- We will use `json.load()` and `json.dump()` - **without s here**
### read  from file
```python
import json

with open("file.json", "r") as f:
    x = json.load(f)

print(x) # dictionary
print(type(x)) # <class 'dict'>
```
### write to file
`json.dump(data, file)`
```python
import json

# a Python object (dict):  
x = {  
    "name": "John",  
    "age": 30,  
    "city": "New York"  
}

with open("file.json", "w") as f:
    json.dump(x, f, indent=4)
```

## Serialization and Deserialization Class
```python
import json

class MyClass:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Create an instance of MyClass
obj = MyClass("John", 30)

# Serialize the object to a JSON string
serialized_obj = json.dumps(obj.__dict__)

# Deserialize the object from the JSON string
loaded_obj_dict = json.loads(serialized_obj)
loaded_obj = MyClass(**loaded_obj_dict)

# Now loaded_obj is a deserialized instance of MyClass
print(loaded_obj.name)  # Output: John
print(loaded_obj.age)   # Output: 30
```