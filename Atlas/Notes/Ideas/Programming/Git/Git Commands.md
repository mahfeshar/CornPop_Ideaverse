---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-27
---

# Git Commands
![[Pasted image 20240627115048.png]]
- **git reset**
    
    - _Description_: It resets changes in the working directory. When used with –hard HEAD, this command discards all changes made to the working directory and staging area and resets the repository to the last commit (HEAD).
    - _Syntax_:
        
        - **git reset**
        - **git reset –hard HEAD**

- **git branch**
    
    - _Description_: It lists, creates, or deletes branches in a repository. To delete the branch, first check out the branch using **git checkout** and then run the command to delete the branch locally.
    - _Syntax_:
        - **git branch** (to list branches)
        - **git branch \<new-branch>** (to create a new branch)
        - **git branch -d \<branch-name>** (to delete a branch)

- `git remote` ⇒ show all remotes
   `-v` ⇒ to have links and know all things

- When you do `git push` it should be like `git push remote_name branch_name`

- `git pull repo_name` ⇒ if any changes done and you want to be up to date

- `git config` ⇒ a lot of configs you can change it 
  `-l` ⇒ show all configs 
  `--global` ⇒ config type 
  `--unset` ⇒ to reset it to default 
  `--edit` ⇒ to edit it by editor 
  e.g. `git config --global user.name "mahmoud"`

- `git status` ⇒ working tree status

- `git add . or *` to add all files and all new changes

- `git config --global alias.st status` ⇒ to make a shortcut for status to be st

- **git diff**
    
    - _Description_: It shows changes between commits, commit and working tree, etc. It also compares the branches.
        
    - _Syntax_:
        
        - **git diff** (shows the difference between the working directory and the last commit)
        - **git diff HEAD~1 HEAD** (shows the difference between the last and second-last commits)
        - **git diff \<branch-1> \<branch-2>** (compares the specified branches)

- **git revert**
    
    - _Description_: It reverts a commit by applying a new commit. This will create a new commit that undoes the changes made by the last commit.
        
    - _Syntax_: **git revert HEAD**

- **git remote**
    
    - _Description_: It lists the names of all remote repositories associated with your local repository.
        
    - _Syntax_: **git remote**

[Commands](https://author-ide.skills.network/render?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJtZF9pbnN0cnVjdGlvbnNfdXJsIjoiaHR0cHM6Ly9jZi1jb3Vyc2VzLWRhdGEuczMudXMuY2xvdWQtb2JqZWN0LXN0b3JhZ2UuYXBwZG9tYWluLmNsb3VkL0lCTVNraWxsc05ldHdvcmstQ0QwMTMxRU4tQ291cnNlcmEvbGFicy9SZWFkaW5nL0dpdF9Db21tYW5kcy5tZCIsInRvb2xfdHlwZSI6Imluc3RydWN0aW9uYWwtbGFiIiwiYWRtaW4iOmZhbHNlLCJpYXQiOjE3MTE1NjIxNDZ9.gHnezrNW_H4jkJoqovtjntjDStParkM4_VXmPAqx37E)
[Commands](https://author-ide.skills.network/render?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJtZF9pbnN0cnVjdGlvbnNfdXJsIjoiaHR0cHM6Ly9jZi1jb3Vyc2VzLWRhdGEuczMudXMuY2xvdWQtb2JqZWN0LXN0b3JhZ2UuYXBwZG9tYWluLmNsb3VkL0lCTVNraWxsc05ldHdvcmstQ0QwMTMxRU4tQ291cnNlcmEvbGFicy9DaGVhdF9zaGVldC9NMi9Vc2luZ19HaXRfQ29tbWFuZHNfYW5kX01hbmFnaW5nX0dpdEh1Yl9Qcm9qZWMubWQiLCJ0b29sX3R5cGUiOiJpbnN0cnVjdGlvbmFsLWxhYiIsImFkbWluIjpmYWxzZSwiaWF0IjoxNzExNTYyMTUxfQ.-bNnJD0ERYBds3KP4FwIYMOMMGfkhRXd9W5NrU-GaDk)
[Glossary](https://author-ide.skills.network/render?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJtZF9pbnN0cnVjdGlvbnNfdXJsIjoiaHR0cHM6Ly9jZi1jb3Vyc2VzLWRhdGEuczMudXMuY2xvdWQtb2JqZWN0LXN0b3JhZ2UuYXBwZG9tYWluLmNsb3VkL0lCTVNraWxsc05ldHdvcmstQ0QwMTMxRU4tQ291cnNlcmEvbGFicy9Nb2R1bGUyL0dsb3NzYXJ5L1VzaW5nR2l0Q29tbWFuZHNhbmRNYW5hZ2luZ0dpdEh1YlByb2plY3QubWQiLCJ0b29sX3R5cGUiOiJpbnN0cnVjdGlvbmFsLWxhYiIsImFkbWluIjpmYWxzZSwiaWF0IjoxNzExNTYyMTQ0fQ.1178BL0vbpj6gYtdEsGD-fy1XK1EuBULx16a0yIhWio)
## Branching:

- `git branch` ⇒ all branch will appear

- `git branch branch_name` ⇒ create a new branch

- `git checkout branch_name` ⇒ go to the another branch

- `git checkout -b branch_name` ⇒ will create a branch and go to it

- `git branch -d branch_name` ⇒ to delete the branch `-d` ⇒ small لو فيه تعديل متعملش مش هيتحذف `-D` ⇒ capital لو فيه تعديل لسا متعملش هيحذف البرانش عادي

- `git branch -m new_name` ⇒ rename the branch

To merge:

1. Go to the main branch
2. Write `git merge branch_name`
3. push `git push`

> If the same file has difference in main and branch, he will tell you. and you should go to this file and change it to what you want. and then make `git pull`

If you pushed from the branch -not from main-, he will make pull request