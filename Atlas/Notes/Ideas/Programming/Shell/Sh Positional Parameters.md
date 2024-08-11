---
up:
  - "[[Shell MOC]]"
related: 
created: 2024-05-20
tags:
---
[Positional Parameters](https://www.adminschoice.com/bash-positional-parameters)
- We can use it at shell script.
### $0, $1 $2 $3 
- $0: File name
- $1 $2 $3: To get the specific argument from the script
```sh
#!usr//bin/bash
echo “File name is ” $0
echo “First arg. is ” $1
echo “Second arg. is ” $2
echo “Third arg. is ” $3
echo “Fourth arg. is ” $4

$ ./test.sh aa bb cc dd
File name is ./test.sh
First arg. is aa
Second arg. is bb
Third arg. is cc
Fourth arg. is dd
```
### $*
- Lists all the command line parameters in a single string
```sh
#!/usr/bin/bash
echo "All (*) args are " $*

./test.sh aa bb cc dd  
All (*) args are aa bb cc dd
```
### $@
- Lists all command line parameters in a array format
```sh
echo "Array of args are " $@

_./test.sh aa bb cc dd_  
_Array of args are aa bb cc dd_
```
- The difference between $* and $@ is that $*  gives out a single string output whereas $@ gives a list format output .
### $\#
- Number of command line arguments
```sh
echo "Number of args. (#) are " $#

./test.sh aa bb cc dd  
Number of args. ( # ) are 4
```
### $?
- Returns the exit status of last executed process.
- $? parameter returns 0 for success and non zero for error conditions.
```sh
#!/usr/bin/bash
ls
echo "Exit status is: " $?

./test.sh  
letters osmodule rpms testfile txt1  
Exit status is : **0**

#!/bin/sh  
las ## non existing command  
echo “Exit status is : ” $?

./test.sh  
./test.sh: line 2: las: command not found  
Exit status is : 127
```
### $!
- Gives the process ID of the last job placed into the background
```sh
$tail -f txt1 &

$ jobs  
[1]+ Running tail -f txt1.log  &      ### still running in background

$echo $!    ### get the process id 
5378

$ps -ef | grep 5378  #### confirm if this is the same process id
work 5378 4406 0 23:33 pts/0 00:00:00 tail -f txt1.log
```

### $\$
- Expands to the process ID of the shell or invoking shell in case of subshell.
```sh
test.sh  
#!/bin/sh  
echo “Shell process id is : ” $$

./test.sh  
Shell process id is : 5103    
#### it gives the process id of the sub subshell when script executed.

or  
$ echo $$  
4406                        
#### This is process id of the invoking shell, bash in this case.

$ ps -ef | grep 4406  
work 4406 4402 0 22:38 pts/0 00:00:00 bash       
#### confirmation of pid
```
### $_
- Gives shell script names or command line argument for the last command executed.
```sh
ls -ltr  
total 156  
drwxr-xr-x. 2 work work 4096 Jun 20 2015 Templates  
drwxr-xr-x. 2 work work 4096 Jun 20 2015 Public  
drwxr-xr-x. 2 work work 4096 Jun 20 2015 Pictures  
drwxr-xr-x. 2 work work 4096 Jun 20 2015 Music

$ echo $_  
-ltr                 ###    it gives command line parameters

$ ./test.sh  
$ echo $_  
./test.sh     ### Gives file name for shell scripts
```
- We used it at [[Sh Mkdir and cd to it (same line)]]
### $-
- List special parameters set for bash.

This is the default flag set returned :

```sh
$echo $-  
himBH
```

h : hash all, remember the locations of commands it has found through querying your PATH.  
i : interactive shell  
m : monitor jobs in background & foreground  
B : brace expand use the efficient brace expansion in bash.  
H : history expand – enable to use history command and reuse commands from history.

bash options can be added or removed using set command, Ironically + sign removes the option and – sign adds it

```sh
_$ echo $-_  
_himBH_

$ set +H  
[work@localhost ~]$ echo $-  
himB

[work@localhost ~]$ set -H  
[work@localhost ~]$ echo $-  
himBH
```