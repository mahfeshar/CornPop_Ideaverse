---
up:
  - "[[Shell MOC]]"
related:
  - "[[Sh ps command]]"
  - "[[Sh pgrep command]]"
  - "[[Sh Process]]"
created: 2024-04-29
tags:
  - note/develop🍃
Link: https://linuxhint.com/the-pkill-command-in-linux/
---
- It kills program [[Sh Process]]es based on the parameters you specify.
- It does not requite entering the process's PID number like the [[Sh kill command]], you can end that process by entering the process’s name as input.
## Syntax
```sh
pkill [OPTION] <PATTERN>
```
- We specified the matching `<PATTERN>` using an extended regular expression.
## Different ways

| **Command**                   | **Output**                                                                                                                                                                                 |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `pkill -15 process`           | Kill process by process name                                                                                                                                                               |
| `pkill - HUP X`               | Reload Process X                                                                                                                                                                           |
| `pkill -f "X A"`              | Kill Process Based on Full Command                                                                                                                                                         |
| `pkill --signal SIGKILL edge` | By default, the pkill command uses the “SIGTERM” signal during its execution. You can change the default signal                                                                            |
| `pkill -i [process]`          | This command is case-sensitive. To make the pkill case insensitive                                                                                                                         |
| `pkill -u X`                  | Match the processes being run by a specific user                                                                                                                                           |
| `pkill -u X, Y, Z`            | Separate multiple users with commas if you want to specify more than one.                                                                                                                  |
| `pkill -9 -u X Y`             | You can also combine search patterns and options.<br>“X” is the username, and “Y” is the search pattern.                                                                                   |
| `pkill -9 -o screen` or `-n`  | The -o and -n options display the least recently oldest or most recently started processes. (old, new)<br>For example, run the following command to kill the least recently oldest screen: |
### Kill process by process name
- We will use `pkill` with no options and use `15 - TERM` signal to it
```sh
pkill -15 firefox
```
>[!info]
>When one or more running process names match the request, the command returns 0. otherwise, the exit code is 1.
This may be useful when writing a [[Shell MOC]]

### Kill Process Based on Full Command
The `pkill` command matches only process names by default. Through the -f option, we can instruct `pkill` to execute the completed command instead of the process name.

Suppose there are two types of ping commands running in your system, and you will run the following command to stop them:

```sh
pkill ping
```

Both will kill the ping commands running in your system by using the previous command. To avoid this problem, the -f command-line option is used.

```sh
pkill -9-f "ping A"
```

Here, “A” can be any one ping of your system.

The previous command will kill only the ping inputted when it runs.
## With signals
- We can send [[Sh Signal]]s with it by hyphen prefixes the number `-15` or signal name after running `pkill`.
- You can list all available prompts by using the `kill -l` commend.
 
| 15 (TERM): | For stopping any process completely |
| ---------- | ----------------------------------- |
| 9 (KILL):  | For killing a process               |
| 1 (HUP):   | For reloading a process             |
We have three ways to specify signals:
1. Without the “SIG” prefix, such as `-HUP`
2. With the “SIG” prefix like `-SIGHUP`
3. Using a number, such as `–1`
