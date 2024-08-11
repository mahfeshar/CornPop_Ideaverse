---
up:
  - "[[Python MOC]]"
related: 
created: 2024-07-05
---

The arguments of the print function are the following ones:
```python
print(value1, ....., sep=' ', end='\n', file=sys.stdout, flush=False)
```

The print function can print an arbitrary number of values ("value1, value2, ...")
```python
a = 3.14
print("a = ", a)
#output a = 3.14
print("a = \n", a)
#output a = 
#		3.14
```

في الغالب لو لاحظت ان بين كل قيمة والتانية لما بتفصل بينهم ب , بيعمل هو space تلقائي عشان يفصل بينهم
وانت ممكن تغير الموضوع دا عن طريق انك تستخدم [[#sep]]
### sep

```python
print("a", "b")
# a b
print("a", "b", sep="")
#ab
print(192,168,178,42,sep=".")
#192.168.178.42
print("a","b",sep=":-)")
#a:-)b
```
---
### end

كل print بعد ما تخلص بتعمل newline

```python
for i in range(4):
    print(i)
0
1
2
3
```

وانت ممكن تغيرها عن طريق [[#end]]

```python
for i in range(4):
     print(i, end=" :-) ")
0 :-) 1 :-) 2 :-) 3 :-)
```
---

### file

The output of the print function is send to the standard output stream (sys.stdout) by default.
By redefining the keyword parameter "file" we can send the output into a different stream e.g. sys.stderr or a file:

```python
fh = open("data.txt","w")
print("42 is the answer, but what is the question?", file=fh)
fh.close()
```

We can see that we don't get any output in the interactive shell. The output is sent to the file "data.txt".

It's also possible to redirect the output to the standard error channel this way:

```python
import sys
# output into sys.stderr:

print("Error: 42", file=sys.stderr)

Error: 42
```

We can [[Py Format for print]] output in many ways.