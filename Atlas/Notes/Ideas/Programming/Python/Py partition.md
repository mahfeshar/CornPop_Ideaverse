---
up:
  - "[[Py String]]"
related:
  - "[[Py split]]"
  - "[[Py strip]]"
created: 2024-05-17
tags: 
---
- Search for a specified string, and splits the string into a tuple containing three elements.
	- The first element contains the part before the specified string.
	- The second element contains the specified string.
	- The third element contains the part after the string.
>[!Note]
> This method searches for the _first_ occurrence of the specified string.

- Syntax: `string.partition(value)`
	- value: The string to search for

```python
txt = "I could eat bananas all day"  
x = txt.partition("bananas")  
print(x) # ('I could eat ', 'bananas', ' all day')

x = txt.partition("apples")
print(x) # ('I could eat bananas all day', '', '')
```