---
up:
  - "[[Shell MOC]]"
related: 
created: 2024-05-08
tags:
  - note/develop🍃
---

- Append means simply add the data to the file without erasing existing data.
## using >> operator
- The `>>` operator redirects output to a file. 
- If the mentioned file doesn’t exist the file is created and then the text is appended to the file.
- We can use [[Sh echo]], [[Sh printf]] to append text into a file
```sh
echo "Which is the best Linux Distro?"  >>  file.txt
printf "Which is the best Linux Distro?\n"  >>  file.txt
```
- We can use [[Sh cat]] to append the content of one file to another file
```sh
cat file1.txt >> file2.txt
```
> [!info]
> Don’t use **>** of **>>** This will erase the data of the target file. This may cause data loss.

## Using tee Command
- We can use [[Sh tee command]] which copies the text from standard input and writes it to the standard output file.
- The tee provides `-a` option to append the text to the file.
```sh
echo "Which is the best Linux Distro?"   | tee -a file.txt
cat file1.txt | tee -a file2.txt
```