---
up:
  - "[[Py Magic methods]]"
related:
  - "[[Py __str__]]"
  - "[[Py __dict__]]"
  - "[[Py __init__]]"
  - "[[Py __repr__]]"
  - "[[Py __class__]]"
created: 2024-04-26
tags:
---

- Return the length of the container.
```python
class Skill:
  def __init__(self):
    self.skills = ["Html", "Css", "Js"]

  def __str__(self): 
    return f"This is My Skills => {self.skills}"

  def __len__(self):
    return len(self.skills)

profile = Skill()
print(len(profile)) # 3
```