---
up:
  - "[[Python MOC]]"
related: 
created: 2024-07-05
---


[32.12. dis — Disassembler for Python bytecode — Python 3.4.10 documentation](https://docs.python.org/3.4/library/dis.html)
[Understanding Python Bytecode. Learn about disassembling Python… | by Reza Bagheri | Towards Data Science (archive.is)](https://archive.is/klORv)
## Intro
The source code of a programming language can be executed using an **interpreter** or a **compiler**. 

### Compiled
In a compiled language, a compiler will translate the source code directly into binary machine code. 
This machine code is specific to that target machine since each machine can have a different operating system and hardware. 
After compilation, the target machine will directly run the machine code.
### Interpreted
In an interpreted language, the source code is not directly run by the target machine. 
There is another program called the interpreter that reads and executes the source code directly. 
The interpreter, which is specific to the target machine, translates each statement of the source code into machine code and runs it.
### Is python compiled or interpreted?
Python is usually called an **interpreted** language, however, **it combines compiling and interpreting**. 
When we execute a source code (a file with a `.py` extension), Python first compiles it into a bytecode. 
The bytecode is a **low-level platform-independent representation** of your source code, however, it is not the binary machine code and cannot be run by the target machine directly. 
In fact, it is a set of **instructions for a virtual machine** which is called the Python Virtual Machine (PVM).
لما بتشغل فايل بايثون بيحوله لbytecode وهو عبارة عن low-level representation بس دا مش باينري كود فميقدرش يشتغل على الجهاز على طول.
هي عبارة عن Instructions لحاجة اسمها PVM

After compilation, the bytecode is sent for execution to the PVM. 
The PVM is an **interpreter that runs the bytecode** and is part of the Python system. 
The bytecode is platform-independent, but PVM is specific to the target machine. 
The default implementation of the Python programming language is **CPython** which is written in the C programming language.
بعد ما بيحصل compile الbytecode اللي اتعمل بيروح لPVM عشان نقدر نشغله وهو عبارة عن Interpreter
CPython compiles the python source code into the bytecode, and this bytecode is then executed by the CPython virtual machine.
## Generating bytecode file
In Python, the bytecode is stored in a `.pyc` file. 
In Python 3, the bytecode files are stored in a folder named `__pycache__`. 
This folder is automatically created when you try to import another file that you created:
```python
import file_name
```

However, it will not be created if we don't import another file in the source code. 
In that case, we can still manually create it. 

---
To compile the individual files `file_1.py` to `file_n.py` from the command line, we can write:
```python
python -m compileall file_1.py ... file_n.py
```

All the generated `pyc` files will be stored in the `__pycache__` folder. 
If you provide no file names after `compileall,` it will compile all the python source code files in the current folder.
### Compile()
We can also use the `compile()` function to compile a string that contains the Python source code. 
The syntax of this function is:

```python
compile(_source_,_filename_,_mode_,_flag_,_dont_inherit_,_optimize_)
```

We only focus on the first three arguments which are required (the others are optional). 
`source` is the source code to compile which can be a String, a Bytes object, or an AST object. 
`filename` is the name of the file that the source code comes from. 
If the source code does not come from a file, you can write whatever you like or leave an empty string. `mode` can be:

- `'exec'`: accepts Python source code in any form (any number of statements or blocks). It compiles them into a bytecode that finally returns `None`

- `'eval'` : accepts a single expression and compiles it into a bytecode that finally returns the value of that expression

- `'single'`: only accepts a single statement (or multiple statements separated by `;`). If the last statement is an expression, then the resulting bytecode prints the `repr()` of the value of that expression to the standard output.

For example, to compile some Python statements we can write:
`s=''' a=5 a+=1 print(a) ''' compile(s, "", "exec")`
or equivalently write:
`compile("a=5 \na+=1 \nprint(a)", "", "exec")`

To evaluate an expression we can write:
`compile("a+7", "", "eval")`

This mode gives an error if you don't have an expression:
`# This does not work: compile("a=a+1", "", "eval")`

Here `a=a+1` is not an expression and does not return anything, so we cannot use the `eval` mode. However, we can use the `single` mode to compile it:
`compile("a=a+1", "", "single")`

But what is returned by `compile`? When you run the `compile` function, Python returns:
`<code object <module> at 0x000001A1DED95540, file "", line 1>`

So what the `compile` function is returning is a _code object_ (the address after `at` can be different on your machine).

#### Code object
The `compile()` function returns a Python code object. Everything in Python is an object. For example we you define an integer variable, its value is stored in an `int` object and you can easily check its type using the `type()` function:
`a = 5 type(a)  # Output is: int`

In a similar way, the bytecode generated by the compile function is stored in the `code` object.
`c = compile("a=a+1", "", "single") type(c)  # Output is: code`

The code object contains not only the bytecode but also some other information necessary for the CPython to run the bytecode (they will be discussed later). A code object can be executed or evaluated by passing it to the `exec()` or `eval()` function. So we can write:
`exec(compile("print(5)", "", "single"))  # Output is: 5`

When you define a function in Python, it creates a code object for it and you can access it using the `__code__` attribute. For example, we can write:
`def f(n):     return n f.__code__`  

And the output will be:
`<code object f at 0x000001A1E093E660, file "<ipython-input-61-88c7683062d9>", line 1>`

Like any other objects the code object has some attributes, and to get the bytecode stored in a code object, you can use its `co_code` attribute:
```python
c = compile("print(5)", "", "single") 
c.co_code
```

The output is:
`b'e\x00d\x00\x83\x01F\x00d\x01S\x00'`

The result is a _bytes literal_ which is prefixed with `b'.` It is an immutable sequence of bytes and has a type of `bytes`. Each byte can have a decimal value of 0 to 255. So a bytes literal is an immutable sequence of integers between 0 to 255. Each byte can be shown by an ASCII character whose character code is the same as the byte value or it can be shown by a leading `\x` followed by two characters. The leading `\x` escape means that the next two characters are interpreted as hex digits for the character code. 

For example:
`print(c.co_code[0]) chr(c.co_code[0])`
gives:
`101 'e'`

since the first element has the decimal value of 101 and can be shown with the character `e` whose ASCII character code is 101. Or:
`print(c.co_code[4]) chr(c.co_code[4])`
gives:
Copy`131 '\x83'`

since the 4th element has the decimal value of 131. The hexadecimal value of 131 is 83. So this byte can be shown with a character whose character code is `\x83`.

![None](https://miro.medium.com/v2/resize:fit:700/1*XSMRlTXxKxm8BpRteSHBMg.jpeg)

These sequences of bytes can be interpreted by CPython, but they are not human-friendly. So we need to understand how these bytes are mapped to the actual instructions that will be executed by CPython. In the next section, we are going to disassemble the byte code into some human-friendly instruction to see how the bytecode is executed by CPython.
## Bytecode details
- The bytecode can be thought of as a series of instructions or a low-level program for the Python interpreter. 
- After version 3.6, Python uses 2 bytes for each instruction.
- One byte is for the code of that instruction which is called an _opcode_, and one byte is reserved for its argument which is called the _oparg._ 
- Each opcode has a human-friendly name which is called the _opname_.
```python
opcode oparg  
opcode oparg  
.  
.  
.
```
### Opname 
- تقدر تقول كل رقم بيعرفك ال opname بتاعك يعني كل رقم بيرمز لعملية معينة
- تقدر تعرف الopname من خلال ال `dis`
- فيه شوية instructions مش بتحتاج argument وعشان كدا الbyte بتاع الarg بيتشال
  الopcodes اللي القيمة بتاعها أقل من رقم معين مش بتحتاج argument والرقم دا هو 90
  So the opcodes >=`dis.HAVE_ARGUMENT` have an argument, and the opcodes < `dis.HAVE_ARGUMENT` ignore it.
```python
# we have a short bytecode `b'd\x00Z\x00d\x01S\x00'`
# We can easily show their decimal value:
bytecode = b'd\x00Z\x00d\x01S\x00'  
for byte in bytecode:  
	print(byte, end=' ') # 100 0 90 0 100 1 83 0
```
- عشان أعرف ال opname هستخدم زي ما قولت ال `dis`
```python
import dis
# Prev code
print(dis.opname[100]) # LOAD_CONST
```
- الرقم بتاع العملية أكبر من ال `dis.HAVE_ARGUMENT` فكدا احنا عندنا Argument وبيتعبر عنها بالرقم اللي بعدها على طول اللي هو فوق 0
- خد بالك ممكن الرقم يبقا مكتوب 0 83 فكدا المفروض ال 83 أقل من 90 فملوش arg بس جنبه واحد فأنا بهمله
#### Arguments beig than byte
- In addition, some of the instructions can have an argument too big to fit into the default one byte.
- في الحالة دي بزود opname اسمه `EXTENDED_ARG` وهو بيبقا عبارة عن shifting ناحية ال left بمقدار 8
![[Pasted image 20240414130328.png]]
- وبعد كدا بزود عليها اللي بعدها يعني لو عايز ال argument يبقا ب260 يبقا هخلي ال extended ب 1 وازود 4
- There is a special opcode `144` to handle these instructions. Its opname is `EXTENDED_ARG`, and it is also stored in `dis.EXTENDED_ARG`. 
- This opcode prefixes any opcode which has an argument bigger than one byte. 
- For example, suppose that we have the opcode 131 (its opname is `CALL_FUNCTION`) and its oparg needs to be 260. So it should be:
```python
CALL_FUNCTION 260 # WRONG
```
- However, the maximum number that a byte can store is 255, and 260 does not fit into a byte. So this opcode is prefixed with `EXTENDED_ARG`:
```python
EXTENDED_ARG 1  
CALL_FUNCTION 4
```
- When the interpreter executes `EXTENDED_ARG`, its oparg (which is 1) is left-shifted by eight bits and stored in a temporary variable. Let’s call it `extended_arg` (do not confuse it with the opname `EXTENDED_ARG`):
```python
extened_arg = 1 << 8  # same as 1 * 256
```
- So the binary value `0b1` (the binary value of 1) is converted to `0b100000000`. This is like multiplying 1 by 256 in the decimal system and `extened_arg` will be equal to 256. Now we have two bytes in `extened_arg`. When the interpreter reaches to the next instruction, this two-byte value is added to its oparg (which is 4 here) using a bitwise `or`.
```python
extened_arg = extened_arg | 4  
# Same as extened_arg += 4
```
This is like adding the value of the oparg to `extened_arg`. So now we have:
```python
extened_arg = 256 + 4 = 260
```
and this value will be used as the actual oparg of `CALL_FUNCTION`. So, in fact,
```python
EXTENDED_ARG 1  
CALL_FUNCTION 4

# is interpreted as:

EXTENDED_ARG 1  
CALL_FUNCTION 260
```
- For each opcode, at most three prefixal `EXTENDED_ARG` are allowed, forming an argument from two-byte to four-byte.
- 
