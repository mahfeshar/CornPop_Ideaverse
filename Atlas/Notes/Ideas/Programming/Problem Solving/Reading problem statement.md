---
up:
  - "[[Problem Solving|Problem Solving]]"
related: 
created: 2024-09-01
---

Although we read it fast, it is one of popular reason for failure!
	The best way to avoid that is to be organized - to have a **DISIPLINE** during reading: a systematic way of reading

1- Read the problem slowly and think in each statement.
1.1- Make sure every statement does not conflict what you overall understood
1.2- Re-think in a statement, If it seems a tricky statement
1.3- Number All important details

2- In some problems, constraints are clear (e.g. topcoder & IOI), some times they are not.
2.1 Each time you read a constraint in mid of description, write it beside.
2.2 Never to avoid any constraints, especially unusual one (e.g. $2*(a+b) < c$). Try to know why such constraints.
2.3 Sometimes constraints make problem a special case of a general one. While general may not be solvable, a specific one could be.
2.4- Ignoring constraints may push you approach problem trivially while it needs careful work ($n <= 10^18$)
2.5- Ignoring constraints may push you approach problem complicatedly while it could be solved trivially ($n <= 10$)
2.6- Sometimes constraints are not direct
2.6.1- Find triangle angle with 2 precision -> $360 * 10^2$	(angle * 2^precision)
2.7- Sometimes more input space analysis is needed: Given a string of (a, b, c) chars & length <= n -> we have $3^n$ possible string

3- Trace Samples as long as they are traceable
3.1- Many times students write solutions and find samples doesn't work. They have to debug
3.1.1- Sometimes they have code mistakes and original idea is correct
3.1.1- Sometimes they have code mistakes and original idea has some flaws
3.1.1- Sometimes they have code mistakes and original idea is incorrect!
3.2- Sometimes samples are trivial and mislead you.

4- If text is not small, Re-read the problem statement once. Make sure you you have the full picture.

5- Think in missed cases. Most of times authors don't put all basic cases. Think in them.

6- Think in boundary & Especial cases. They are big source of WAs & RTEs
6.1 Think in the smallest boundaries (e.g. n = 0, 1, 2 - $R*C = {1*1, 1*2, 2*1, 2, 2}$ - str = "", str = "a", ...)
6.2 Think in the largest boundaries (e.g. n = MAX, array is fully, string has max characters, ...)
6.3 Think in especial cases (array filled with zeros, ...)

7- Tips
7.1- NEVER to assume something not mentioned.
	(E.g. given $a <= 100$ - then a may be < 0 - Find count in range $[a, b]$ - then b may be < a)
7.2- Make sure that you know exactly what is output and its "format"