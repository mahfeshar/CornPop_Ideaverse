---
up:
  - "[[Py String]]"
related:
  - "[[Py split]]"
  - "[[Py partition]]"
created: 2024-05-17
tags: 
---

- Remove any leading, and trailing whitespaces
- Leading means at the beginning of the string, trailing means at the end.
- You can specify which character(s) to remove, if not, any whitespaces will be removed.
- لو فيه حاجة فالنص مش هيشيلها هو هيشيل اللي قبلها واللي بعدها بس
- Syntax: `string.strip(characters)`

```python
txt = "     banana     "  
x = txt.strip()  
print("of all fruits", x, "is my favorite") # banana

txt = ",,,,,rrttgg.....banana....rrr"  
x = txt.strip(",.grt")  
print(x) # banana
```