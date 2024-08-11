---
up:
  - "[[Shell MOC]]"
related: 
created: 2024-07-25
---
**Note:** Linux and the UNIX system are case-sensitive

![[Pasted image 20240725142107.png]]

### ls
- List the contents of a directory

`ls [option] [file/directory]`

| Options      | Output                                                                                                        |
| ------------ | ------------------------------------------------------------------------------------------------------------- |
| `-l`         | Long format                                                                                                   |
| `-a`         | All files include hidden files                                                                                |
| `-la`        | Long format and hidden                                                                                        |
| `-n`         | User and group IDs displayed numerically                                                                      |
| `ls -m`      | Comma-separated values                                                                                        |
| `-h`         | Print file sizes in human-readable format (e.g., 1K, 234M, 2G).                                               |
| `-p`<br>`-F` | List the directories with a trailing forward slash e.g. `bin/`                                                |
| `-t`         | Sort files and directories by their last modification time, displaying the most recently modified ones first. |
| `-r`         | Known as **reverse order** which is used to reverse the default order of listing.                             |
| `-S`         | Sort files and directories by their sizes, listing the largest ones first.                                    |
| `-R`         | List files and directories recursively, including subdirectories.                                             |
| `-i`         | Known as `inode` which displays the index number (`inode`) of each file and directory.                        |
| `-g`         | Known as **group** which displays the group ownership of files and directories instead of the owner.          |
| `-d`         | List directories themselves, rather than their contents.                                                      |

#### A closer look at long format:
```tsx
-rw-------   1 me       me            576 Apr 17  2019 weather.txt
drwxr-xr-x   6 me       me           1024 Oct  9  2019 web_page
-rw-rw-r--   1 me       me         276480 Feb 11 20:41 web_site.tar
-rw-------   1 me       me           5743 Dec 16  2018 xmas_file.txt

----------     -------  -------  -------- ------------ -------------
    |             |        |         |         |             |
    |             |        |         |         |         File Name
    |             |        |         |         |
    |             |        |         |         +---  Modification Time
    |             |        |         |
    |             |        |         +-------------   Size (in bytes)
    |             |        |
    |             |        +-----------------------        Group
    |             |
    |             +--------------------------------        Owner
    |
    +----------------------------------------------   File Permissions
```

File Permissions:
- First character ⇒ the type of file (d means directory, - means regular - ordinary file) 
- The second set (every 3 letters ⇒ read, write, execution) 
- Rights for owner, rights for group, rights for everybody else.

Some facts : 
1. File names that begin with a period character are hidden. e.g. (.config) 
2. File names in Linux, like Unix, are case sensitive. The file names "File1" and "file1" refer to different files.
### less
- This is a program that let’s us to view text files 
  just write `less file_name` this will display the file

| **Command**        | **Action**                                                                      |
| ------------------ | ------------------------------------------------------------------------------- |
| Page Up or b       | Scroll back one page                                                            |
| Page Down or space | Scroll forward one page                                                         |
| G                  | Go to the end of the text file                                                  |
| 1G                 | Go to the beginning of the text file                                            |
| /_characters_      | Search forward in the text file for an occurrence of the specified _characters_ |
| n                  | Repeat the previous search                                                      |
| h                  | Display a complete list less commands and options                               |
| q                  | Quit                                                                            |
### file 
- It’s helpful to determine what kind of data a file contains before we try to view it.
- Syntax: `file name_of_file`

| **File Type**                  | **Description**                                               | **Viewable as text?**                  |
| ------------------------------ | ------------------------------------------------------------- | -------------------------------------- |
| ASCII text                     | The name says it all                                          | yes                                    |
| Bourne-Again shell script text | A `bash` script                                               | yes                                    |
| ELF 64-bit LSB executable      | An executable binary program                                  | no                                     |
| ELF 64-bit LSB shared object   | A shared library                                              | no                                     |
| GNU tar archive                | A tape archive file. A common way of storing groups of files. | no, use `**tar tvf**` to view listing. |
| gzip compressed data           | An archive compressed with `**gzip**`                         | no                                     |
| HTML document text             | A web page                                                    | yes                                    |
| JPEG image data                | A compressed JPEG image                                       | no                                     |
| PostScript document text       | A PostScript file                                             | yes                                    |
| Zip archive data               | An archive compressed with `**zip**`                          | no                                     |
### Some other commends :

1. `cat` ⇒ appear content of text file in terminal
2. `man` ⇒ to know a lot of information about any commend
3. `clear` ⇒ to clear terminal