---
up:
  - "[[Shell MOC]]"
related: 
created: 2024-05-12
tags:
---

## What are "Commands"?
Commands can be one of 4 different kinds:

1. **An executable program** like all those files we saw in /usr/bin. 
   Within this category, programs can be _compiled binaries_ such as programs written in C and C++, or programs written in _scripting languages_ such as the shell, Perl, Python, Ruby, etc.
2. **A command built into the shell itself.** bash provides a number of commands internally called _shell builtins_. 
   The **`cd`** command, for example, is a shell builtin.
3. **A shell function.** These are miniature مصغر shell scripts incorporated إدماج into the _environment_. 
4. **An alias.** Commands that we can define ourselves, built from other commands.

## Identifying Commands
### type
- It's a shell builtin that displays the kind of command the shell will execute.
- Syntax: `type command`
```sh
type type
type is a shell builtin

type ls
s is aliased to `ls --color=auto'

type cp
cp is /bin/cp
```
### which
- To determine the exact location of a given executable
- Sometimes there is more than one version of an executable program installed on a system. While this is not very common on desktop systems, it's not unusual on large servers.
```sh
which ls
/bin/ls
```
>[!note]
> `which` only works for executable programs, not builtins nor aliases that are substitutes for actual executable programs.

## Command Documentation
### help
- `bash` has a built-in help facility available for each of the shell _builtins_.
- **Help command itself offers three options:**
    - **d:** display only a brief description of the specified command.
    - **m:** organize the available information just as the **man command** does.
    - **s:** display the command syntax of the specified command.

- **Syntax 📝**
    
    - `$**help** [OPTION]... [COMMAND NAME]...`
        
    - **help command**
        
        - Displays brief summaries of builtin commands.
            
        - `$helphelp`
            
            ```bash
            ┌──(kali㉿kali)-[~]
            └─$ help --help 
            help: help [-dms] [pattern ...]
                Display information about builtin commands.
            
                Displays brief summaries of builtin commands.  If PATTERN is
                specified, gives detailed help on all commands matching PATTERN,
                otherwise the list of help topics is printed.
            
                Options:
                  -d        output short description for each topic
                  -m        display usage in pseudo-manpage format
                  -s        output only a short usage synopsis for each topic matching
                            PATTERN
            
                Arguments:
                  PATTERN   Pattern specifying a help topic
            
                Exit Status:
                Returns success unless PATTERN is not found or an invalid option is given.
            ```
            
            ```bash
            ┌──(kali㉿kali)-[~]
            └─$ help help
            help: help [-dms] [pattern ...]
                Display information about builtin commands.
            
                Displays brief summaries of builtin commands.  If PATTERN is
                specified, gives detailed help on all commands matching PATTERN,
                otherwise the list of help topics is printed.
            
                Options:
                  -d        output short description for each topic
                  -m        display usage in pseudo-manpage format
                  -s        output only a short usage synopsis for each topic matching
                            PATTERN
            
                Arguments:
                  PATTERN   Pattern specifying a help topic
            
                Exit Status:
                Returns success unless PATTERN is not found or an invalid option is
            ```
            
            - `We get everything we want to know about help command`
    - **help -d command**
        
        - Using the -d option to output short description for each topic
            
        - `$help -d``help`
            
            ```bash
            ┌──(kali㉿kali)-[~]
            └─$ help -d help 
            help - Display information about builtin commands.
            ```
            
            - We can see that -d flag gives a one line description for the command mentioned.
    - **help -m command**
        
        - Using the -m option to output in pseudo-manpage format
            
        - `$help -m``help`
            
            ```bash
            ┌──(kali㉿kali)-[~]
            └─$ help -m help 
            NAME
                help - Display information about builtin commands.
            
            SYNOPSIS
                help [-dms] [pattern ...]
            
            DESCRIPTION
                Display information about builtin commands.
            
                Displays brief summaries of builtin commands.  If PATTERN is
                specified, gives detailed help on all commands matching PATTERN,
                otherwise the list of help topics is printed.
            
                Options:
                  -d        output short description for each topic
                  -m        display usage in pseudo-manpage format
                  -s        output only a short usage synopsis for each topic matching
                            PATTERN
            
                Arguments:
                  PATTERN   Pattern specifying a help topic
            
                Exit Status:
                Returns success unless PATTERN is not found or an invalid option is given.
            
            SEE ALSO
                bash(1)
            
            IMPLEMENTATION
                GNU bash, version 5.1.16(1)-release (x86_64-pc-linux-gnu)
                Copyright (C) 2020 Free Software Foundation, Inc.
                License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
            ```
            
            - The -m flag gives the output in manpage like format. Man is system’s manual viewer.
    - **help -s command**
        
        - Using -s option to output only a short usage synopsis
            
        - `$help -s``help`
            
            ```bash
            ┌──(kali㉿kali)-[~]
            └─$ help -s help 
            help: help [-dms] [pattern ...]
            ```
            
            - -s flag displays the command syntax of the specified command.

### --help
- Many executable programs support a “--help” option that displays a description of the command's supported syntax and options
```bash
[me@linuxbox me]$ **mkdir --help**
Usage: mkdir [OPTION] DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.
Mandatory arguments to long options are mandatory for short options
too.

   -Z, --context=CONTEXT (SELinux) set security context to CONTEXT
   -m, --mode=MODE   set file mode (as in chmod), not a=rwx – umask
   -p, --parents     no error if existing, make parent directories as
                     needed
   -v, --verbose     print a message for each created directory
   --help            display this help and exit
   --version         output version information and exit
```
### man
- Most executable programs intended for command line use provide a formal piece of documentation called a _manual or man page_.
- It provides a detailed view of the command which includes `NAME, SYNOPSIS, DESCRIPTION, OPTIONS, EXIT STATUS, RETURN VALUES, ERRORS, FILES, VERSIONS, EXAMPLES, and AUTHORS`
- **Every manual is divided into the following sections:**
    - Executable programs or shell commands
    - System calls (functions provided by the kernel)
    - Library calls (functions within program libraries
    - Games
    - Special files (usually found in /dev)
    - File formats and conventions eg /etc/passwd
    - Miscellaneous (including macro packages and conventions), e.g. groff(7)
    - System administration commands (usually only for root)
    - Kernel routines [Non standard]
#### Syntax
- Syntax: `$man [OPTION]... [COMMAND NAME]...`
- **No Option**
    
    - **No Option**: It displays the whole manual of the command.
        
    - `$**man** [COMMAND NAME]`
        
        In this example, manual pages of the command ‘_printf_‘ are simply returned.
        
        ```bash
        ┌──(kali㉿kali)-[~]
        └─$ **man** printf
        
        NAME
               printf - format and print data
        
        SYNOPSIS
               printf FORMAT [ARGUMENT]...
               printf OPTION
        
        DESCRIPTION
               Print ARGUMENT(s) according to FORMAT, or execute according to OPTION:
        
               --help display this help and exit
        
               --version
                      output version information and exit
        
               FORMAT controls the output as in C printf.  Interpreted sequences are:
        
               \\"     double quote
        
               \\\\     backslash
        
               \\a     alert (BEL)
        
               \\b     backspace
        
               \\c     produce no further output
        
         Manual page printf(1) line 1 (press h for help or q to quit)
        ```
        
- **Section-num**
    
    - **Section-num**: Since a manual is divided into multiple sections so this option is used to display only a specific section of a manual.
        
    - `$**man** [SECTION-NUM] [COMMAND NAME]`
        
        In this example, the manual pages of command ‘printf‘ are returned which lies in the section 3.
        
        ```bash
        ┌──(kali㉿kali)-[~]
        └─$ **man 3** printf
        
        printf(3)                                      Library Functions Manual                                     printf(3)
        
        NAME
               printf, fprintf, dprintf, sprintf, snprintf, vprintf, vfprintf, vdprintf, vsprintf, vsnprintf - formatted out‐
               put conversion
        
        LIBRARY
               Standard C library (libc, -lc)
        
        SYNOPSIS
               #include <stdio.h>
        
               int printf(const char *restrict format, ...);
               int fprintf(FILE *restrict stream,
                           const char *restrict format, ...);
               int dprintf(int fd,
                           const char *restrict format, ...);
               int sprintf(char *restrict str,
                           const char *restrict format, ...);
               int snprintf(char str[restrict .size], size_t size,
                           const char *restrict format, ...);
        
               int vprintf(const char *restrict format, va_list ap);
               int vfprintf(FILE *restrict stream,
                           const char *restrict format, va_list ap);
               int vdprintf(int fd,
                           const char *restrict format, va_list ap);
               int vsprintf(char *restrict str,
                           const char *restrict format, va_list ap);
         Manual page printf(3) line 1 (press h for help or q to quit)
        
        ```
        
- **-f option**
    
    - **Section-num**: Since a manual is divided into multiple sections so this option is used to display only a specific section of a manual.
        
    - `$**man**-f [COMMAND NAME]`
        
        In this example, the manual pages of command ‘printf‘ are returned which lies in the section 3.
        
        ```bash
        ┌──(kali㉿kali)-[~]
        └─$ **man -f printf
        printf (1)           - format and print data
        printf (3)           - formatted output conversion**
        
        ```
        
- **-a option**
    
    - **-a option:** This option helps us to display all the available intro manual pages in succession.
    - Display, in succession, all of the available manual pages contained within the manual. It is possible to quit between successive displays or skip any of them.
        - `$**man**-a [COMMAND NAME]`
            
            ```bash
            ┌──(kali㉿kali)-[~]
            └─$ man -a intro
            --Man-- next: intro(8) [ view (return) | skip (Ctrl-D) | quit (Ctrl-C) ]
            
            --Man-- next: intro(32) [ view (return) | skip (Ctrl-D) | quit (Ctrl-C) ]
            ```
            
            - Note:📝 in this example, you can move through the manual pages(sections) either reading(by pressing Enter) skipping(by pressing ctrl+D), or exiting(by pressing ctrl+C).
- **-k option**
    
    - This option searches the given command as a regular expression in all the manuals and it returns the manual pages with the section number in which it is found.
        - `$**man**-k [COMMAND NAME]`
            
            ```bash
            ┌──(kali㉿kali)-[~]
            └─$ man -k printf
            PA_CHAR (3const)     - define custom behavior for printf-like functions
            PA_DOUBLE (3const)   - define custom behavior for printf-like functions
            PA_FLAG_LONG (3const) - define custom behavior for printf-like functions
            PA_FLAG_LONG_DOUBLE (3const) - define custom behavior for printf-like functions
            PA_FLAG_LONG_LONG (3const) - define custom behavior for printf-like functions
            PA_FLAG_PTR (3const) - define custom behavior for printf-like functions
            PA_FLAG_SHORT (3const) - define custom behavior for printf-like functions
            PA_FLOAT (3const)    - define custom behavior for printf-like functions
            PA_INT (3const)      - define custom behavior for printf-like functions
            PA_LAST (3const)     - define custom behavior for printf-like functions
            PA_POINTER (3const)  - define custom behavior for printf-like functions
            PA_STRING (3const)   - define custom behavior for printf-like functions
            PA_WCHAR (3const)    - define custom behavior for printf-like functions
            PA_WSTRING (3const)  - define custom behavior for printf-like functions
            asprintf (3)         - print to allocated string
            dprintf (3)          - formatted output conversion
            fprintf (3)          - formatted output conversion
            fwprintf (3)         - formatted wide-character output conversion
            printf (1)           - format and print data
            printf (3)           - formatted output conversion
            printf.h (3head)     - define custom behavior for printf-like functions
            register_printf_modifier (3) - define custom behavior for printf-like functions
            printf_arginfo_size_function (3type) - define custom behavior for printf-like functions
            printf_function (3type) - define custom behavior for printf-like functions
            printf_info (3type)  - define custom behavior for printf-like functions
            printf_va_arg_function (3type) - define custom behavior for printf-like functions
            register_printf_specifier (3) - define custom behavior for printf-like functions
            register_printf_type (3) - define custom behavior for printf-like functions
            snprintf (3)         - formatted output conversion
            sprintf (3)          - formatted output conversion
            swprintf (3)         - formatted wide-character output conversion
            vasprintf (3)        - print to allocated string
            vdprintf (3)         - formatted output conversion
            vfprintf (3)         - formatted output conversion
            vfwprintf (3)        - formatted wide-character output conversion
            vprintf (3)          - formatted output conversion
            vsnprintf (3)        - formatted output conversion
            vsprintf (3)         - formatted output conversion
            vswprintf (3)        - formatted wide-character output conversion
            vwprintf (3)         - formatted wide-character output conversion
            wprintf (3)          - formatted wide-character output conversion
            XtAsprintf (3)       - memory management functions
            ```
            
            - Search the short descriptions and manual page names for the keywordprintf as regular expression. Print out any matches. Equivalent toaproposprintf.
- **-w option**
    
    - **-w option**: This option returns the location in which the manual page of a given command is present.
        
    - `$**man -w** [COMMAND NAME]`
        
        ```bash
        ┌──(kali㉿kali)-[~]
        └─$ man -w ls
        /usr/share/man/man1/ls.1.gz
        
        ┌──(kali㉿kali)-[~]
        └─$ man --where ls
        /usr/share/man/man1/ls.1.gz
        
        ┌──(kali㉿kali)-[~]
        └─$ man --path ls
        /usr/share/man/man1/ls.1.gz
        
        ┌──(kali㉿kali)-[~]
        └─$ man --location ls
        /usr/share/man/man1/ls.1.gz
        ```
        - Don't actually display the manual page, but do print the location of the source nroff file that would be formatted. If the -a option is also used, then print the locations of all source files that match the search criteria.
- **-I option**
    - **-I option**: It considers the command as case sensitive.
    - `$**man**-I [COMMAND NAME]`
    
	    ```bash
	    ┌──(kali㉿kali)-[~]
	    └─$ man -I printf
	    PRINTF(1)                                           User Commands                                           PRINTF(1)
	    
	    NAME
	           printf - format and print data
	    
	    SYNOPSIS
	           printf FORMAT [ARGUMENT]...
	           printf OPTION
	    
	    DESCRIPTION
	           Print ARGUMENT(s) according to FORMAT, or execute according to OPTION:
	    
	           --help display this help and exit
	    
	           --version
	                  output version information and exit
	    
	           FORMAT controls the output as in C printf.  Interpreted sequences are:
	    
	           \\"     double quote
	    
	           \\\\     backslash
	    
	           \\a     alert (BEL)
	    
	           \\b     backspace
	    
	           \\c     produce no further output
	    
	     Manual page printf(1) line 1 (press h for help or q to quit)
	    ```
    
    - `Search for manual pages case-sensitively.`

RTFM → Read The Fucking Manual

![[Pasted image 20240725151723.png]]

