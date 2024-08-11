---
up:
  - "[[Python MOC]]"
related:
  - "[[Py package]]"
  - "[[Py Module]]"
  - "[[Py library]]"
created: 2024-04-28
tags:
---

`__name__` => Built In variable
`__main__` => Value of the `__name__` variable

## Executions Methods
عشان تفهم بس عندنا طريقتين عشان تشغل فايل مكتوب بالبايثون
1- Directly => Execute the Python File Using the Command Line
2- From Import => Import The Code From File To Another File [[Py package]], [[Py Module]]

في الطريقة ال Directly دي بقا قيمة ال `__name__` بتتحط ب `__main__`
At directly execution the `__name__ == __main__`
```python
print(__name__) 
# if u executed it directly, the output will be __main__
```

### How to use it and why?
To prevent code in your script from being executed when imported
```python
if __name__ == "__main__":
	print("Directly")
	#write code here
```