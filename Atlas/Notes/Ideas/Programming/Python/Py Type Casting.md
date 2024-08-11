---
up:
  - "[[Python MOC]]"
related: 
created: 2024-07-05
---

انك تغير من نوع لنوع تاني بكل بساطة
هحول ال float ل int

```python
kg = 4.5 #float

print(int(kg)) #int

ord('a') #97
chr(97) #'a'
```

You can use it with [[Py Format for print]]
```python
for i in range(97, 123):
	if i == 101 or i == 113:
	        continue
	print("{:c}".format(i), end='')
```

## string to int
```python
# int
num = '10'
print(type(num)) # string

converted_num = int(num)
print(type(converted_num)) # int

# eval
a = "100"
print(eval(a) + 12)

# isdigit
string = "42"
if string.isdigit():
	integer = int(string)
	print(integer) # Output: 42
else:
	print(f"{string} is not a valid integer.")
```