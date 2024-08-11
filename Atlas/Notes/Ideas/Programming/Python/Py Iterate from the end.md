---
up:
  - "[[Python MOC]]"
related: 
created: 2024-07-24
---

Iterating through an array (or list) from the end in Python can be done in several ways. Here are a few common methods:

### Method 1: Using a `for` loop with `reversed()`
```python
arr = [1, 2, 3, 4, 5]

for element in reversed(arr):
    print(element)
```

### Method 2: Using a `for` loop with a negative step in slicing
```python
arr = [1, 2, 3, 4, 5]

for element in arr[::-1]:
    print(element)
```

### Method 3: Using a `while` loop
```python
arr = [1, 2, 3, 4, 5]
i = len(arr) - 1

while i >= 0:
    print(arr[i])
    i -= 1
```

### Method 4: Using a `for` loop with `range()` and a negative step
```python
arr = [1, 2, 3, 4, 5]

for i in range(len(arr) - 1, -1, -1):
    print(arr[i])
```

Each of these methods will iterate through the list from the last element to the first element, printing each element along the way. Choose the one that best fits your coding style and needs.