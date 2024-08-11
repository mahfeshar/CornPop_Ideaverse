---
up:
  - "[[Shell MOC]]"
related:
  - "[[Sh If Statements]]"
  - "[[Sh Case]]"
created: 2024-04-29
tags: 
---

- إستخدامها:  أفضل أحاول في أمر معين لحد ما يوصل للنتيجة اللي انا عايزها
## While loops
```shell
while[<some test>]
do
	<commands>
done
```
![[Pasted image 20240307095915.png]]
```shell
#!/bin/bash

#initialise the variable counter with it's starting value.
counter=1 #لازم تبقا لازقة فيها

while [ $counter -le 10 ] #(counter is less than or equal to 10)
do
	echo $counter
	((counter++))
done

echo All done
```

In the example above we could have put `-lt` as opposed to `-le` (less than as opposed to less than or equal). Had we done this it would have printed up until 9.

## Until Loops
- شبه ال while بالظبط، الفرق ان دي هيفضل ينفذ الأمر لحد ما الشرط يبقا true
```shell
#!/bin/bash

counter=1
until [ $counter -gt 10 ]
do
	echo $counter
	((counter++))
done
```
- والحكمة من وجود الاتنين مع انهم بيعملوا نفس الحاجة عشان يخلي الفهم أسهل مش أكتر
**Leave the towel on the line until it's dry.**
**Leave the towel on the line while it is not dry.**

## For Loops
مختلفة شوية عن الاتنين اللي فوق
```shell
for var in <list>  
do  
	<commands>  
done
```

The list is defined as a series of strings, separated by spaces.
```shell
#!/bin/bash

names='Corn Pop Mahmoud'

for name in $names
do
	echo $name
done
# Corn Pop Mahmoud
```

فيه طريقة كمان ممكن نعملها بيها زي ال cpp
```shell
#!/bin/bash

for ((num = 1; num <= 5; num++))
do
	echo $num
done
#1 2 3 4 5
```

من التطبيقات القوية على ال for اننا نستخدمها مع ال files عن طريق ال [[wildcars]]
```shell
#!/bin/bash
# Make a php copy of any html files

for value in $1/*.html
do
	cp $value $1/$( basename -s .html $value ).php
done
```
## Ranges
- زي list من الأرقام
```shell
#!/bin/bash

for value in {1..5}
do
	echo $value
done
# 1 2 3 4 5
```

- وممكن برضو تحط قيمة الزيادة أو النقصان اللي انت عايزها، لو بدأت بالرقم الكبير كدا هينقص مش هيزود
```shell
#!/bin/bash

for value in {10..0..2}
do
	echo $value
done
# 10 8 6 4 2 0
```
## Controlling Loops: Break and Continue
### Break
بتقول للاسكريبت يوقف ال loop بشرط معين

```shell
#!/bin/bash
# Make a backup set of files

for value in $1/*
do
	used=$( df $1 | tail -1 | awk '{ print $5 }' | sed 's/%//' )
	if [ used -gt 90 ]
	then
		echo Low disk space 1>&2
		break
	fi
	cp $value $1/backup/
done
```

### Continue
بتخليه ميكملش الدورة دي ويعملها skip ويروح للي بعدها
```shell
#!/bin/bash
# Make a backup set of files

for value in $1/*
do
	if [ ! -r $value ]
	then
		echo $value not readable 1>&2
		continue
	fi
	cp $value $1/backup/
done
```

## Select
- بياخد input من اليوزر ويشوف الرقم اللي اختارته دا رقم كام في ال list ويبدأ ينفذ على أساسه
```shell
#!/bin/bash

names='Corn Pop Mahmoud Quit'

PS3='Select number: '

select name in $names
do
	if [ $name == 'Quit' ]
	then
		break
	fi
	echo Hello $name
done
echo Bye
```
- No error checking is done. If the user enters something other than a number or a number not corresponding to an item then **var** becomes null (empty)
- If the user hits _enter_ without entering any data then the list of options will be displayed again.
- The loop will end when an EOF signal is entered or the *break statement* is issued.
- You may change the system variable **PS3** to change the prompt that is displayed.
## Summary
*while do done*
Perform a set of commands while a test is true.

*until do done*
Perform a set of commands until a test is true.

*for do done*
Perform a set of commands for each item in a list.

*break*
Exit the currently running loop.

*continue*
Stop this iteration of the loop and begin the next iteration.

*select do done*
Display a simple menu system for selecting items from a list.

*Clarity*
There are several Bash loop mechanisms. Pick the one which makes your code the easiest to follow.

*Planning*
Now that your scripts are getting a little more complex you will probably want to spend a little bit of time thinking about how you structure them before diving in.