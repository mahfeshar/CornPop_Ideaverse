---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-27
---


## Git Staging Environment
whenever you hit a milestone or finish a part of the work, you should add the files to a Staging Environment.

**Staged** files are files that are ready to be **committed** to the repository you are working on. You will learn more about [[Git Commit]] shortly.

### Add
```shell
git add index.html
```
The file should be **Staged**.
```shell
git status 
On branch master 

No commits yet Changes to be committed:   

	(use "git rm --cached ..." to unstage)     
		new file: index.html
```

We can add all files if we have a lot of files.
```shell
git add -all
or
git add -A
or
git add .
```
Now all files are added to the staging environment, and we are ready to do our first [[Git Commit]]