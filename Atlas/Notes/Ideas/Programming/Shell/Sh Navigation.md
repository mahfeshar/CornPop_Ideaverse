---
up:
  - "[[Shell MOC]]"
related: 
created: 2024-07-25
---

To open terminal: 
1. Search about "[[Sh What is 'the Shell'#What's a "Terminal"?|Terminal]]"
2. From keyboard: `ctrl + alt + t`
To exit from terminal:
1. Write "exit"
2. From Keyboard: `ctrl + D`
## File system organization
- You should know that this is hierarchical directory (the directory is a folder in windows)

![[Pasted image 20240508142428.png]]
- The main or the first directory is known as “root”

- **/**
    
    - `The /` in the instruction above refers to the _**root**_ directory. The **root directory** is the one from which all other directories branch off from
        
    - _show me only the 1st Level of the directory tree starting at / (**root**)_
        
        ```bash
        ┌──(kali㉿kali)-[~]
        └─$ tree / -L 1
        /
        ├── bin -> usr/bin
        ├── boot
        ├── dev
        ├── etc
        ├── home
        ├── initrd.img -> boot/initrd.img-6.1.0-kali9-amd64
        ├── initrd.img.old -> boot/initrd.img-6.1.0-kali5-amd64
        ├── lib -> usr/lib
        ├── lib32 -> usr/lib32
        ├── lib64 -> usr/lib64
        ├── libx32 -> usr/libx32
        ├── lost+found
        ├── media
        ├── mnt
        ├── opt
        ├── proc
        ├── root
        ├── run
        ├── sbin -> usr/sbin
        ├── srv
        ├── sys
        ├── tmp
        ├── usr
        ├── var
        ├── vmlinuz -> boot/vmlinuz-6.1.0-kali9-amd64
        └── vmlinuz.old -> boot/vmlinuz-6.1.0-kali5-amd64
        
        23 directories, 4 files
        
        ┌──(kali㉿kali)-[~]
        └─$
        ```
- _**/bin**_
    
    - Unlike /sbin, the bin directory contains several useful commands that are of use to both the system administrator as well as non-privileged users.
    - It usually contains shells like bash, csh, etc.... and commonly used commands like cp, mv, rm, cat, ls. For this reason and in contrast to /usr/bin, the binaries in this directory are considered to be essential
- **/etc**
    
    - This is the nerve center of your system, it contains all system related configuration files in here or in its sub-directories. A "configuration file" is defined as a local file used to control the operation of a program;
    - it must be static and cannot be an executable binary. For this reason, it's a good idea to backup this directory regularly.
    - It will definitely save you a lot of re-configuration later if you re-install or lose your current installation. Normally, no binaries should be or are located here.
- **/sbin**
    
    - Linux discriminates between 'normal' executables and those used for system maintenance and/or administrative tasks. The latter reside either here or - the less important ones - in /usr/sbin. Locally installed system administration programs should be placed into /usr/local/sbin.
    - Programs executed after /usr is known to be mounted (when there are no problems) are generally placed into /usr/sbin. This directory contains binaries that are essential to the working of the system. These include system administration as well as maintenance and hardware configuration programs. You may find lilo, fdisk, init, ifconfig, etc.... here.
- **/tmp**
    
    - This directory contains mostly files that are required temporarily. Many programs use this to create lock files and for temporary storage of data.
    - Do not remove files from this directory unless you know exactly what you are doing! Many of these files are important for currently running programs and deleting them may result in a system crash. Usually, it won't contain more than a few KB anyway.
    - On most systems, this directory is cleared out at boot or at shutdown by the local system.
- **/usr/bin**
    
    - This directory contains the vast majority of binaries on your system. Executables in this directory vary widely. For instance vi, gcc, gnome-session and mozilla and are all found here.
- **/usr/share**
    
    - **This directory contains 'shareable', architecture-independent files (docs, icons, fonts etc).**
    - **📝 Note, however, that '/usr/share' is generally not intended to be shared by different operating systems or by different releases of the same operating system.**
    - **Any program or package that contains or requires data that doesn't need to be modified should store that data in '/usr/share' (or '/usr/local/share', if installed locally). It is recommended that a subdirectory be used in /usr/share for this purpose.”**
- **$PATH**
    
    - PATH is an _environmental variable_ in Linux and other Unix-like operating systems that tells the _shell_ which directories to search for _executable files_ (i.e., ready-to-run programs) in response to commands issued by a user.
## Some important commands
Any commend be in form: `commend -options arguments`
### Navigation
1. `pwd`: print working directory
2. `cd` change directory: It is used to change the current directory of the terminal
We will discuss [[Sh Pathnames]]
#### cd

| Command                                 | Output                               |
| --------------------------------------- | ------------------------------------ |
| `cd -`                                  | Previous directory                   |
| `cd ..`                                 | Go back one step  (parent directory) |
| `cd ~user_name`<br>or `cd`<br>or `cd ~` | Go to the home directory             |
| `cd /`                                  | Go to root directory                 |
```bash
┌──(kali㉿kali)-[~]
└─$  cd Downloads
┌──(kali㉿kali)- [~/Downloads]
└─$
```
