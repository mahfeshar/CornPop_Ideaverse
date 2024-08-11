---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-01
---
## WriteLine
 - دي هتطبع وهتعمل newline بعدها عادي جدا 
- ممكن تستخدم أكتر واحدة مع بعض

```cs
Console.WriteLine("Hello World!");
```

- عشان تطبع variable في النص فيه أكتر من طريقة منها انك تعمل concatenate أو انك تستخدم `{}` أو تستخدم `$`

```cs
Console.WriteLine("Hello Mr " + Name + " - Your age is " + Age);
Console.WriteLine("Hello Mr {0} - Your age is {1}", Name, Age);
```
## Write
لو مش عايز ينزل للسطر اللي بعده ممكن نستخدم دي 
```cs
Console.Write("Hello World! ");
Console.Write("I will print on the same line.");
```

