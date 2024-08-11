---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-27
---


## Git Install
You can download Git for free from the following website: [GIT](https://git-scm.com/)

## Configure Git
```shell
git config --global user.name "w3schools-test" 
git config --global user.email "test@w3schools.com"
git config --list #to list all config info
```

**Note:** Use `global` to set the username and e-mail for **every repository** on your computer.
If you want to set the username/e-mail for just the current repo, you can remove `global`

## Initialize Git
Once you have navigated to the correct folder, you can initialize Git on that folder:
```shell
git init
```

**Note:** Git now knows that it should watch the folder you initiated it on.
Git creates a hidden folder to keep track of changes.
Now let's move to add [[Git New Files]]

## Status
We will create a new file and know about status for this folder
```GIT
touch new.txt
git status
# untracked files:
	new.txt
```

## Track the Changes in file
```GIT
git add .
git commit file_name -m "Commit message"
git commit -a -m "Commit message" # commit without staging
git log --oneline

git diff

code .gitignore
# all files we don't want git to track it (*.bak - *~)

```

Add everything that's currently in this repository to your list of files that you're tracking

```shell
mkdir css
touch css/.git-keep
# This file that GIT doesn't care about but that let's Git know that it does want to be tracking this file structure
# Git doesn't track empty folders

git commit --amend --no-edit
# For small changes, same commit but that typo will be fixed 
git log
# if you used it, there's no more new commits
```