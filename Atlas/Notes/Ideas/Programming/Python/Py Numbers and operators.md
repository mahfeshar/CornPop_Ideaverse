---
up:
  - "[[Python MOC]]"
related: 
created: 2024-07-05
---


+, -, * and / can be used to perform arithmetic; parentheses (()) can be used for grouping

```Python
2 + 2
4
50 - 5 * 6
20
(50 - 5*6)/4
5.0
8/5 # dvision always returns a floating point number
1.6
```
The integer numbers (e.g. 2, 4, 20) have type int, the ones with a fractional part (e.g. 5.0, 1.6) have type float.

Division (/) always returns a float. To do floor division and get an integer result you can use the // operator; to calculate the remainder you can use %.
```Python
17 / 3 # classic division returns a float 
5.666666666666667 
17 // 3 # floor division discards the fractional part 
5 
17 % 3 # the % operator returns the remainder of the division 
2 
5 * 3 + 2 # floored quotient * divisor + remainder 
17
```

### Powers
it is possible to use the ** operator to calculate powers.
```Python
5 ** 2 # 5 squared
25
2**7 # 2 to the power of 7
128
```

### Equal sign
The equal sign (=) is used to assign a value to a variable. 
Afterwards, no result is displayed before the next interactive prompt
```Python
width = 20 
height = 5 * 9 
width * height 
900
```

> If a variable is not “defined” (assigned a value), trying to use it will give you an error

There is full support for floating point; operators with mixed type operands convert the integer operand to floating point

```Python
4 * 3.75 - 1 
14.0
```

> [!Note]
> In interactive mode, the last printed expression is assigned to the variable `_`. 
> This means that when you are using Python as a desk calculator, it is somewhat easier to continue calculations

```python

tax = 12.5 / 100
price = 100.50
price * tax
12.5625
price + _
113.0625
round(_, 2)
113.06
```

المفروض انك تعامل ال variable دا على انه read only يعني مينفعش تحط فيه قيمة
ممكن تعمل local variable بنفس الاسم بس دا هيختفي

