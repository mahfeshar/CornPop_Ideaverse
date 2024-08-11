---
up:
  - "[[Python MOC]]"
related: 
created: 2024-08-02
---

## Many Ways for a Nicer Output
We will try to create a nicer output in Python.
> The best one to use is "[[#string format]]"

## String modulo %
- It also called "string interpolation", because it interpolates يقحم various class types (like  int, float and so on) into a formatted string.
- But ==Don't use it== and use [[#string format]]
![[string-module.png]]
The values can be literals, variables or arbitrary arithmetic expressions
![[string-modue-2.png]]
The general syntax for a format placeholder is `%[flags][width][.precision]type'
![[Placeholders.png]]
خد بالك من الحتة دي ان الرقم اللي عاليمين دا عدد كل ال placeholders ومن ضمنها الأرقام العشرية وكمان العلامة بتاخد مكان
> There is no difference between "d" and "i" both are used for formatting integers.

![[placeholders-multiline.png]]
### Conversion rules
| Conversion  | Meaning  |
|---|---|
|d|Signed integer decimal.|
|i|Signed integer decimal.|
|o|Unsigned octal.|
|u|Obsolete and equivalent to 'd', i.e. signed integer decimal.|
|x|Unsigned hexadecimal (lowercase).|
|X|Unsigned hexadecimal (uppercase).|
|e|Floating point exponential format (lowercase).|
|E|Floating point exponential format (uppercase).|
|f|Floating point decimal format.|
|F|Floating point decimal format.|
|g|Same as "e" if exponent is greater than -4 or less than precision, "f" otherwise.|
|G|Same as "E" if exponent is greater than -4 or less than precision, "F" otherwise.|
|c|Single character (accepts integer or single character string).|
|r|String (converts any python object using repr()).|
|s|String (converts any python object using str()).|
|%|No argument is converted, results in a "%" character in the result.|
```python
print("%10.3e" % (356.08977))
# 3.561e+02
print("%10.3E" % (356.08977))
#3.561E+02
print("%10o"% (25))
#        31
print("%10.3o"% (25))
#       031
print("%10.5o"% (25))
#     00031
print("%5x"% (47))
#   2f
print("%5.4x"% (47))
# 002f
print("Only one percentage sign: %% " % ())
#Only one percentage sign: %
print("%#5X"% (47))
# 0X2F
print("%5X"% (47))
#   2F
print("%#5.4X"% (47))
#0X002F
print("%#5o"% (25))
# 0o31
print("%+d"% (42))
#+42
print("% d"% (42))
# 42
print("%+2d"% (42))
#+42
print("% 2d"% (42))
# 42
print("%2d"% (42))
#42

```

If the string modulo operator is applied to a string, it returns a string.
first create a formatted string, which will be assigned to a variable and this variable is passed to the print function:
```python
s = "Price: $ %8.2f"% (356.08977)
print(s)
#Price: $   356.09
```

## String format

The general form of this method looks like this: `template.format(p0, p1, ..., k0=v0, k1=v1, ...)`

بيبقا عندك باختصار شوية اقواس في الكود وبتبدأ تحطلها القيم بتاعها جوا كلمة format
>If a brace character has to be printed, it has to be escaped by doubling it: `{{ and }}`.

ال arguments دي بتبقا متقسمة ل positional arguments (0, 1, 2) وهكذا
انت ممكن تستخدم وانت بتكتب ال string جوا كل قوسين تحدد دا تبع انهي postion ولو متحددش وسيبته فاضي فهو هيمشي بالترتيب
وممكن اعرف كل واحد ب key معين واكتب جوا ال format كل key بتشاور على ايه

- وممكن جوا القوسين دول برضو نعمل format زي ما اتعلمنا في [[#Conversion rules]] عن طريق اني اكتب {0:5d} والصفر دا عبارة عن ال position وجنبه ال format بتاعه

![[method-format.png]]

![[method-format-key.png]]
### Examples
```python
"First argument: {0}, second one: {1}".format(47,11)
'First argument: 47, second one: 11'

"Second argument: {1}, first one: {0}".format(47,11)
'Second argument: 11, first one: 47'

"Second argument: {1:3d}, first one: {0:7.2f}".format(47.42,11)
'Second argument:  11, first one:   47.42'

"First argument: {}, second one: {}".format(47,11) 
# arguments can be used more than once:
'First argument: 47, second one: 11'

"various precisions: {0:6.2f} or {0:6.3f}".format(1.4148)
'various precisions:   1.41 or  1.415'

"Art: {a:5d},  Price: {p:8.2f}".format(a=453, p=59.058)
'Art:   453,  Price:    59.06'
```

### Flags

| Flag  | Meaning  |
|---|---|
|#|Used with o, x or X specifiers the value is preceded with 0, 0o, 0O, 0x or 0X respectively.|
|0|The conversion result will be zero padded for numeric values.|
|-|The converted value is left adjusted|
||If no sign (minus sign e.g.) is going to be written, a blank space is inserted before the value.|
|+|A sign character ("+" or "-") will precede the conversion (overrides a "space" flag).|

### Options

| Option | Meaning                                                                                                                                                                                                                                                                                                                                                               |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| '<'    | The field will be left-aligned within the available space. This is usually the default for strings.                                                                                                                                                                                                                                                                   |
| '>'    | The field will be right-aligned within the available space. This is the default for numbers.                                                                                                                                                                                                                                                                          |
| '0'    | If the width field is preceded by a zero ('0') character, sign-aware zero-padding for numeric types will be enabled.<br><br>```Python<br>>>> x = 378<br>>>> print("The value is {:06d}".format(x))<br>The value is 000378<br>>>> x = -378<br>>>> print("The value is {:06d}".format(x))<br>The value is -00378<br>```                                                 |
| ','    | This option signals the use of a comma for a ==thousands== separator.<br><br>```Python<br>>>> print("The value is {:,}".format(x))<br>The value is 78,962,324,245<br>>>> print("The value is {0:6,d}".format(x))<br>The value is 5,897,653,423<br>>>> x = 5897653423.89676<br>>>> print("The value is {0:12,.3f}".format(x))<br>The value is 5,897,653,423.897<br>``` |
| '='    | Forces the padding to be placed after the sign (if any) but before the digits. This is used for printing fields in the form "+000000120". This alignment option is only valid for numeric types.                                                                                                                                                                      |
| '^'    | Forces the field to be centered within the available space.                                                                                                                                                                                                                                                                                                           |
| '+'    | indicates that a sign should be used for both positive as well as negative numbers.                                                                                                                                                                                                                                                                                   |
| '-'    | indicates that a sign should be used only for negative numbers, which is the default behavior.                                                                                                                                                                                                                                                                        |
| space  | indicates that a leading space should be used on positive numbers, and a minus sign on negative numbers.                                                                                                                                                                                                                                                              |
```Python
"{0:<20s} {1:6.2f}".format('Spam & Eggs:', 6.99)
'Spam & Eggs:           6.99'

"{0:>20s} {1:6.2f}".format('Spam & Eggs:', 6.99)
'        Spam & Eggs:   6.99'
```

### Using Dictionary

ممكن نستخدم ال [[Py Dictionaries]] في ال format
```python
data = dict(province="Ontario",capital="Toronto")
data
{'province': 'Ontario', 'capital': 'Toronto'}

print("The capital of {province} is {capital}".format(**data))
The capital of Ontario is Toronto
```

> The double "*" in front of data turns data automatically into the form 'province="Ontario",capital="Toronto"'.

```python
capital_country = {"US": "Washington",
				   "Canada": "Ottawa",
				   "Germany": "Berlin"
}

print("Countries and their capitals:")
for c in capital_country:
	print("{country}: {capital}".format(country=c, capital=capital_country[c]))
```

We can rewrite the previous example by using the dictionary directly. The output will be the same:
```python
for c in capital_country:
    format_string = c + ": {" + c + "}" 
    print(format_string.format(**capital_country))
```



### Local

هي عبارة عن function بنستخدمها عشان أخزن فيها [[Py Dictionaries]] لل current scope's local variables
the local variable names are the keys of this dictionary and the corresponding values are the values of these variables

```python
a = 42
b = 47
def f():
	return 42
locals()

{'a': 50, 'b': 60} #example
```

```python
print("a={a}, b={b} and f={f}".format(**locals()))
a=42, b=47 and f=<function f at 0x00000285FFA729D8>
```
## Other string methods
We have some methods also to format: `ljust, rjust, center and zfill`
### center
بيحط النص بتاعي في النص وبتحدد عدد الخانات اللي انت عايزة ياخدها
```python
s = "python"
s.center(10)
'  Python  '

#we can put any char to fill empty place-holders
s.center(10,'*')
**python**
```

### ljust
بيحازي الكلام بتاعي ناحية الشمال left وممكن تخلي الأماكن الفاضية بأي حرف انت عايزة برضو
```python
s = "Training"
s.ljust(12)
'Training    '

s.ljust(12,":")
'Training::::'
```

### rjust
نفس اللي فوق بس بتحازي ناحية اليمين
```python
s = "Programming"
s.rjust(15)
'    Programming'

s.rjust(15, "~")
'~~~~Programming'
```



### zfill
دي بنستخدمها عشان نخلي الجزء اللي عالشمال من الرقم باصفار 
```python
account_number = "434"
account_number.zfill(12)
'000043447879'
# can be emulated with rjust:
account_number.rjust(12,"0")
'000043447879'
```

## Formatted String Literals
They are prefixed with an 'f'. The formatting syntax is similar to the format strings accepted by str.format().
The replacement fields are expressions, which are evaluated at run time, and then formatted using the format() protocol. 
It's easiest to understand
```python
price = 11.23
f"Price in Euro: {price}"
'Price in Euro: 11.23'

f"Price in Swiss Franks: {price * 1.086}"
'Price in Swiss Franks: 12.195780000000001'

f"Price in Swiss Franks: {price * 1.086:5.2f}"
'Price in Swiss Franks: 12.20'

for article in ["bread", "butter", "tea"]:
    print(f"{article:>10}:")
	 bread:
    butter:
       tea:
```
### Self-Documenting Expressions
- بستخدم علامة ال = مع المتغير عشان يطلعلي اسم المتغير وعلامة = والقمية
- بستخدم الطريقة دي في الdebug في الغالب
```python
>>> print(f"{variable=}")
variable='Some mysterious value'

>>> print(f"{variable= }")
variable= 'Some mysterious value'

>>> print(f"{variable =}")
variable ='Some mysterious value'
```