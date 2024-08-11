---
up:
  - "[[Python MOC]]"
related: 
created: 2024-05-07
tags:
  - note/develop🍃
---

```python
file = open("fileName", "Mode", encoding=None)
```
Modes
"`a`" Append: Open File for appending files, create file if not exists
"`r`" Read: Open file for read and give **Error** If file is not exists (*default*)
"`w`" Write: Open Fil
e For Writing, Create File If Not Exists
"`r+`" Open file for both reading and writing
"`x`" Create: Create File, Give Error If File Exists

Because UTF-8 is the modern de-facto standard, `encoding="utf-8"` is recommended unless you know that you need to use a different encoding.

>[!note]
>In text mode, the default when reading is to convert platform-specific line endings (`\n` on Unix, `\r\n` on Windows) to just `\n`.
>It is good practice to use the [`with`](https://docs.python.org/3/reference/compound_stmts.html#with) keyword when dealing with file objects. The advantage is that the file is properly closed after its suite finishes, even if an exception is raised at some point. Using `with` is also much shorter than writing equivalent [`try`](https://docs.python.org/3/reference/compound_stmts.html#try)-[`finally`](https://docs.python.org/3/reference/compound_stmts.html#finally) blocks
>If you’re not using the [`with`](https://docs.python.org/3/reference/compound_stmts.html#with) keyword, then you should call `f.close()` to close the file and immediately free up any system resources used by it.

We have to types of paths, Absolute path and Relative path
Relative path: from the file that's I am in.
Absolute path: Starts from root
[[Sh Pathnames]]

>[!error]
>If you want to write relative path you should change working directory

### Read file
```python
myFile = open("filename", "r") # If you didn't write `r` it's ok

print(myFile) # File Data Object
# <_io.TextIOWrapper name='file.txt' mode='r' encoding='cp1252'>
print(myFile.name) # file.txt
print(myFile.mode) # r
print(myFile.encoding) # cp1252

print(myFile.read()) # to read number of characters from the file
# The default value is -1 (all file)
# you can type any number of characters
print(myFile.read(5))

print(myFile.readline()) # To readline
print(myFile.readline()) # It will read the line after prev one
print(myFile.readline(5)) # It will read 5 characters from line and will continue at next one

print(myFile.readlines()) # It will return *list* of lines
print(myFile.readlines(50)) # It also takes characters or bytes

# We can loop through lines, with readlines or with only for
for line in myFile:
	print(line)
	if line.startswith("07):
		break

# Close the file
myFile.close()
```
### Write and append 
write will create file if it's not exist
- It will return the number of characters written. (**write and append**)
```python
myFile = open("file.txt", 'w')

# If there's a file and have contents, it will remove prev and write new
myFile.write("Hello Corn\n")
myFile.write("Hello Pop") 
print(myFile.write("Pop")) # 3

myFile.write("Hello" * 1000)

# Write all list (should have list)
myList = ['Hello', 'Corn', 'Pop'] # You should write \n
myFile.writelines(myList)

## Append
# It's continue writing from the cursor position and it won't remove all file data like write

myFile = open("file.txt", 'a')
myFile.write("Newline\n\n\n")
myFile.write("Corn")
```
### closing file automatically
- It's important to close file after finish with it.  it leaves the file open for an indeterminate amount of time after this part of the code has finished executing.
so we should use `with` 
```python
with opne("myFile.txt") as f:
	for line in f:
		print(line, end="")

f.closed # True : to check if file closed or not
```
After the statement is executed, the file _f_ is always closed.
### important info
#### truncate
To cut some text and remove another, It works with append
```python
myFile.truncate(5)
```
#### cursor
```python
# The position of cursor
print(myFile.tell())

# To change curosr position
myFile.seek(6) 
print(myFile.read()) # It will read from character number 6
```
## os module
It's refer to operating system.
```python
import os

print(os.getcwd()) # current working directory

print(os.path.abspath(__file__)) # # The absolute path for the file
# __file__ means the current file

directoryPath = os.path.dirname(__file__) # The directory for the file

os.chdir(directoryPath) 
# changing directory but changing it for just current file not for all system

os.remove(filePath) # It will remove the file
```
To use paths with raw string we should use `r`