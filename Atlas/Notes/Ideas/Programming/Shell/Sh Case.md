---
up:
  - "[[Shell MOC]]"
related:
  - "[[Sh Loop]]"
  - "[[Sh If Statements]]"
created: 2024-04-29
tags:
  - note/develop🍃
---

- عامله زي ال switch انها بتشوف المتغير بقا بيساوي أي قيمة من اللي هديهاله ولا لا
```shell
case expression in
    pattern1)
        # Commands to execute if expression matches pattern1
        ;;
    pattern2)
        # Commands to execute if expression matches pattern2
        ;;
    pattern3 | pattern4)
        # Commands to execute if expression matches pattern3 or pattern4
        ;;
    *)
        # Default commands to execute if no patterns match
        ;;
esac
```
`*)`: This is the default case

### Example:
```shell
#!/bin/bash

fruit="apple"

case $fruit in
    "apple")
        echo "It's an apple."
        ;;
    "banana")
        echo "It's a banana."
        ;;
    "orange" | "grapefruit")
        echo "It's an orange or a grapefruit."
        ;;
    *)
        echo "Unknown fruit."
        ;;
esac
```