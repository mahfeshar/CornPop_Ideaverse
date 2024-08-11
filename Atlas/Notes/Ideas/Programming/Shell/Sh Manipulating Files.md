### cp
- Copy files and directories
- It can copy single file. 
  e.g. `cp file1 file2` (copy the content of file1 into file2. 
  If file2 doesn’t exist, it is created; otherwise file2 is silently overwritten with the contents of file1) the content of file2 deleted
- It can also copy file or a lot of files to directory by `cp files... directory_name`

| Command                   | Results                                                                                                                                                          |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cp file1 dir1`           | Copy the contents of file1 (into a file named file1) inside of directory dir1.                                                                                   |
| `cp -n files.. directory` | to copy all files but don’t copy what exist already                                                                                                              |
| `cp file1 file2`          | Copies the contents of file1 into file2. If file2 does not exist, it is created; otherwise, file2 is silently overwritten with the contents of file1.            |
| `cp -i file1 file2`       | Like above however, since the "-i" (interactive) option is specified, if file2 exists, the user is prompted before it is overwritten with the contents of file1. |
| `cp -R dir1 dir2`         | Copy the contents of the directory dir1. If directory dir2 does not exist, it is created. Otherwise, it creates a directory named dir1 within directory dir2.    |
### mv
- To moves or renames files

| Command               | Results                                                                                                                                                            |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `mv file1 file2`      | If file2 does not exist, then file1 is renamed file2. If file2 exists, its contents are silently replaced with the contents of file1.                              |
| `mv -i file1 file 2`  | Like above however, since the `"-i"` (interactive) option is specified, if file2 exists, the user is prompted before it is overwritten with the contents of file1. |
| `mv file1 file2 dir1` | The files file1 and file2 are moved to directory dir1. If dir1 does not exist, mv will exit with an error.                                                         |
| `mv dir1 dir2`        | If dir2 does not exist, then dir1 is renamed dir2. If dir2 exists, the directory dir1 is moved within directory dir2.                                              |
The difference between `mv` and `cp` in first case that, the file1 in copy will still here but in move it will be removed
### rm
- To remove files or directories

| Command             | Results                                                                                                                 |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `rm file1 file2`    | Delete file1 and file2.                                                                                                 |
| `rm -i file1 file2` | Like above however, since the "-i" (interactive) option is specified, the user is prompted before each file is deleted. |
| `rm -r dir1 dir2`   | Directories dir1 and dir2 are deleted along with all of their contents.                                                 |
| `-f`                | force, which means that it will ignore any errors or warnings and delete the files without prompting for confirmation   |
- `-r` recursive, which means that it will delete all the files and subdirectories inside the given directory
>[!warning]
> - Linux does not have an undelete command. Once you delete something with rm, it's gone. You can inflict terrific damage on your system with rm if you are not careful, particularly with wildcards.
>- Before you use rm with wildcards, try this helpful trick: construct your command using ls instead. By doing this, you can see the effect of your wildcards before you delete files. After you have tested your command with ls, recall the command with the up-arrow key and then substitute rm for ls in the command.

### rmdir
- To remove __empty__ directories

`-p` remove directory and its ancestors, e.g. `rmdir -p a/b/c` = `rmdir a/b/c a/b a`

### mkdir
- To create directories
- Syntax: `mkdir directories`
### touch
- Change file timestamps and create new files
- A file argument that doesn’t exist is created empty, unless `-c` or `-h` is supplied
- `touch -c file1` do not create any files if it doesn’t exist
### To make new file and add text on it
`echo 'Your text here' > File_name`

### nano
- A user-friendly, simple text editor
- Unlike vim editor or any other command-line editor, it doesn’t have any mode. 
- It has an easy GUI(Graphical User Interface) which allows users to interact directly with the text in spite of switching between the modes as in vim editor
### wildcards
- Since the shell uses filenames so much, it provides special characters to help you rapidly specify groups of filenames. Wildcards allow you to select filenames based on patterns of characters.
![[Pasted image 20240510095117.png]]
![[Pasted image 20240510095154.png]]

|   |   |
|---|---|
|**Command**|**Results**|
|`cp *.txt text_files`|Copy all files in the current working directory with names ending with the characters ".txt" to an existing directory named _text_files_.|
|`mv dir1 ../*.bak dir2`|Move the subdirectory _dir1_ and all the files ending in ".bak" in the current working directory's parent directory to an existing directory named _dir2_.|
|`rm *~`|Delete all files in the current working directory that end with the character "~". Some applications create backup files using this naming scheme. Using this command will clean them out of a directory.|
