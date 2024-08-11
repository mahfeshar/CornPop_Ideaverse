---
up:
  - "[[Shell MOC]]"
related:
  - "[[Sh Loop]]"
  - "[[Sh Case]]"
created: 2024-04-29
tags:
  - note/develop🍃
---

## Basic If
```shell
if [<some test>]
then
	<commands>
fi
```
### Example:
```shell
#!/bin/bash

if [ $1 -gt 100 ] # وانت بتفعل الاسكريبت بتكتب المتغير جنبها
then
	echo Hey that\'s a large number
	pwd
fi

date
```
## Tests
| Operator              | Description                                                           |
| --------------------- | --------------------------------------------------------------------- |
| ! EXPRESSION          | The EXPRESSION is false.                                              |
| -n STRING             | The length of STRING is greater than zero.                            |
| -z STRING             | The lengh of STRING is zero (ie it is empty).                         |
| STRING1 = STRING2     | STRING1 is equal to STRING2                                           |
| STRING1 != STRING2    | STRING1 is not equal to STRING2                                       |
| INTEGER1 -eq INTEGER2 | INTEGER1 is numerically equal to INTEGER2                             |
| INTEGER1 -gt INTEGER2 | INTEGER1 is numerically greater than INTEGER2                         |
| INTEGER1 -lt INTEGER2 | INTEGER1 is numerically less than INTEGER2                            |
| -d FILE               | FILE exists and is a directory.                                       |
| -e FILE               | FILE exists.                                                          |
| -r FILE               | FILE exists and the read permission is granted.                       |
| -s FILE               | FILE exists and it's size is greater than zero (ie. it is not empty). |
| -w FILE               | FILE exists and the write permission is granted.                      |
| -x FILE               | FILE exists and the execute permission is granted.                    |
- **=** is slightly different to **-eq**. (001 = 1) will return false as = does a string comparison (ie. character for character the same) whereas -eq does a numerical comparison meaning (001 -eq 1) will return true.
- When we refer to FILE above we are actually meaning a [path](https://ryanstutorials.net/linuxtutorial/navigation.php). Remember that a path may be absolute or relative and may refer to a file or a directory. [[Sh Pathnames]]
- Because `[ ]` is just a reference to the command **test** we may experiment and trouble shoot with test on the command line to make sure our understanding of its behaviour is correct.
```shell
1. test 001 = 1
2. echo $?
3. 1
4. test 001 -eq 1
5. echo $?
6. 0
7. touch myfile
8. test -s myfile
9. echo $?
10. 1
11. ls /etc > myfile
12. test -s myfile
13. echo $?
14. 0
```