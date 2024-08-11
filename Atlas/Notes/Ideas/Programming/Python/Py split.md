---
up:
  - "[[Py String]]"
related:
  - "[[Py strip]]"
  - "[[Py partition]]"
created: 2024-05-17
tags: 
---
- Split a string into a list
- You can specify the separator, default is any whitespace
- Syntax: `string.split(separator, maxsplit)`
	- `separator`: _Optional_. Specifies the separator to use when splitting the string. 
	  By default any whitespace is a separator
	- `maxsplit`: _Optional_. Specifies how many splits to do. 
	  Default value is -1, which is "all occurrences"

```python
txt = "hello, my name is Peter, I am 26 years old"  
x = txt.split(", ")  
print(x) # ['hello', 'my name is Peter', 'I am 26 years old']
```

```python
txt = "apple#banana#cherry#orange"  

# setting the maxsplit parameter to 1, will return a list with 2 elements!  
x = txt.split("#", 1)  
  
print(x) # ['apple', 'banana#cherry#orange']
```