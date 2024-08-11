---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-27
---


We will add new files to this directory.
## Status
check the Git `status` and see if it is a part of our repo:
```shell
git status 
On branch master 

No commits yet Untracked files:   
	(use "git add ..." to include in what will be committed)  
	index.html 
	
nothing added to commit but untracked files present (use "git add" to track)
```
Files in your Git repository folder can be in one of 2 states:
- Tracked - files that Git knows about and are added to the repository
- Untracked - files that are in your working directory, but not added to the repository

When you first add files to an empty repository, they are all untracked. To get Git to track them, you need to stage them, or add them to the staging environment.

ممكن نخلي الرسالة اللي بتظهر أقصر
```shell
git status --short
```
**Note:** Short status flags are:
- ?? - Untracked files
- A - Files added to stage
- M - Modified files
- D - Deleted files