---
up:
  - "[[Shell MOC]]"
related: 
created: 2024-04-29
tags:
  - note/develop🍃
Link: https://www.linfo.org/pid.html
---
- A PID (process identification number) is automatically assigned to each [[Sh Process]] when it is created on a Unix-like operating system
- We said that A [[Sh Process]] is an _executing_ (i.e., running) instance of a program. Each process is guaranteed ضامن a unique PID, which is always a **non-negative integer**
- The `init` process is the process that will always have the same PID on any session and on any system, and that PID is 1.
  This is because `init` is always the first process on the system and is the ancestor of all other processes.

## Work with PID
- We can use [[Sh ps command]] or `pstree` (which shows the process names and PIDs in a tree diagram)
- We can use also `top` command but it differs in that it continuously updates the information.
- You can know only PID for one process by `pidof` and give the process name as argument.
- To end a program which is frozen or otherwise misbehaving , we will use [[Sh kill command]]
## Information of current processes
- /proc filesystem
- `ls /proc | less`, `cat /proc/1/cmdline`