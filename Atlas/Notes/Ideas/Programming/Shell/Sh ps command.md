---
up:
  - "[[Shell MOC]]"
related:
  - "[[Sh pgrep command]]"
  - "[[Sh Process]]"
  - "[[Sh pkill command]]"
created: 2024-04-29
tags:
  - note/develop🍃
Link: https://www.golinuxcloud.com/ps-command-in-linux/
---
## Introduction to `ps`

- A [[Sh Process]] is any executing (running) instance of a program.
- Linux is a multi-tasking and multi-user operating system that allows running several programs.
- `ps` command in Linux displays a list of currently running processes and their PIDs. 
- `ps` is the short form for **Process Status**.
## Syntax
```shell
$ ps [option]
```
Some options available in `ps` command are as follows:
- **-A**: List all processes on the system
- **-e**: List all processes on the system
- **x**: List processes owned by the current user
- **-f**: List processes with full format
- **u**: Display user-oriented format

| **Command**                          | **Output**                                                                                         |
| ------------------------------------ | -------------------------------------------------------------------------------------------------- |
| `ps`                                 | all processes in the current shell                                                                 |
| `ps -A` or `-e`                      | all running processes                                                                              |
| `ps a`                               | associated with a terminal (TTY)                                                                   |
| `ps T`                               | all processes associated with this terminal only                                                   |
| `ps -a`                              | all processes except both session leaders processes not associated with a terminal                 |
| `ps x`                               | all processes owned by the current user                                                            |
| `ps ax`                              | all running processes in BSD format                                                                |
| `ps -f` or `-F`                      | displays extra full format                                                                         |
| `ps u`                               | user-oriented format and shows the information of the user who owns the processes.                 |
| `ps v`                               | display the processes in the virtual memory format                                                 |
| `ps -u` or `U` or `--user`           | display processes of the specified **effective** user name or ID                                   |
| `ps -U` or `--User`                  | selects the processes by the specified **real** user name or ID                                    |
| `ps -g` or `-group`                  | Display processes by **effective group ID or name**                                                |
| `ps -G` or `--Group`                 | Display processes by **real group ID or name**                                                     |
| `ps p process_ID` or `-p` or `--pid` | List processes by process ID                                                                       |
| `ps --ppid`                          | Display specific process by using the **parent process ID**                                        |
| `ps t` or `-t` or `--tty`            | List processes by terminal type                                                                    |
| `ps e` not `-e`                      | show environment after command                                                                     |
| `ps h`                               | Hide the header of ps command output                                                               |
| `ps --header`                        | Repeat the header lines, one per output page.                                                      |
| `ps f` or `--forest`                 | Display a process tree                                                                             |
| `ps -H`                              | print the process hierarchy                                                                        |
| `ps H`                               | Show threads as if they were processes                                                             |
| `ps -L`                              | Show threads with LWP (lightweight process) and NLWP (number of the lightweight processes) columns |
| `ps L`                               | Show format specifiers                                                                             |
| `ps s`                               | Display signal format                                                                              |
| `ps -M`                              | Display security info                                                                              |

## Different examples to use `ps` command
### list all processes in the current shell
- Use it without any options
```shell
ps
```
![[Pasted image 20240429114656.png]]
- **PID**: It shows the unique process ID.
- **TTY**: It shows the terminal type into which the user is logged in.
- **TIME**: It displays the total time that the process has been running.
- **CMD**: It displays the name of the command that launches the process. 
  As we can notice in the output, the second process is started by the ps command itself.

### list all processes
- Use option `-A` or `-e`
```sh
ps -A
ps -e
```
![[Pasted image 20240429114830.png]]
### list all processes associated with a terminal
- Use option `a`
```sh
ps a
```
![[Pasted image 20240429114935.png]]
- The `T` option allows you to select all processes associated with this terminal only.
```sh
golinux@ubuntu-PC:~$ ps T
    PID TTY      STAT   TIME COMMAND
   1925 pts/1    Ss     0:00 bash
   2200 pts/1    R+     0:00 ps T
```
### list processes not associated with a terminal
```sh
ps -a
```
![[Pasted image 20240429115250.png]]
>[!hint]
>Every process group is in a unique _session_. (When the process is created, it becomes a member of the session of its parent.) By convention, the session ID of a session equals the process ID of the first member of the session, called the _session leader_. A process finds the ID of its session using the system call `getsid()`.

### List all processes in BSD format
- Combine `a` with `x`
```sh
ps ax
```
![[Pasted image 20240429115630.png]]
### Display user-oriented format
```sh
ps u
```
![[Pasted image 20240429120025.png]]

### Display virtual memory format
```sh
ps v
```
**%MEM** shows the amount of memory the process is taking up.
  
![ps command to display virtual memory format](https://www.golinuxcloud.com/wp-content/uploads/ps-command-to-display-virtual-memory-format.png "25 ps command examples in Linux [Cheat Sheet]")
### Display processes by effective User ID or Name
```sh
ps -u user[name or id]
ps -u

ps --user user[name or id]
```
![ps command to display processes by effective user name or id](https://www.golinuxcloud.com/wp-content/uploads/ps-command-to-display-processes-by-effective-user-name.png "25 ps command examples in Linux [Cheat Sheet]")
### Display processes by real group ID or name
```sh
$ ps -G group[name or id]
$ ps --Group group[name or id]
```
![ps command to display processes by real group id or name](https://www.golinuxcloud.com/wp-content/uploads/ps-command-to-display-processed-by-real-group-id-or-name.png "25 ps command examples in Linux [Cheat Sheet]")